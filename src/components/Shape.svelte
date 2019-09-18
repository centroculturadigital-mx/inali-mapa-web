<script>
  export let points
  export let command

  $: d = svgPath(points, command === 'line' ? lineCommand : bezierCommand )

  const svgPath = (points, command) => {  
    const d = points.reduce((acc, point, i, a) => i === 0    
      ? `M ${point[0]},${point[1]}`
      : `${acc} ${command(point, i, a)}`
    , '')  
    return d
  }

  const lineCommand = point => `L ${point[0]} ${point[1]}`

  const line = (pointA, pointB) => {
    const lengthX = pointB[0] - pointA[0]
    const lengthY = pointB[1] - pointA[1]  
    return {
      length: Math.sqrt(Math.pow(lengthX, 2) + Math.pow(lengthY, 2)),
      angle: Math.atan2(lengthY, lengthX)
    }
  }

  const controlPoint = (current, previous, next, reverse) => {  // When 'current' is the first or last point of the array
    // 'previous' or 'next' don't exist.
    // Replace with 'current'
    const p = previous || current
    const n = next || current  // The smoothing ratio
    const smoothing = 0.2  // Properties of the opposed-line
    const o = line(p, n)  // If is end-control-point, add PI to the angle to go backward
    const angle = o.angle + (reverse ? Math.PI : 0)
    const length = o.length * smoothing  // The control point position is relative to the current point
    const x = current[0] + Math.cos(angle) * length
    const y = current[1] + Math.sin(angle) * length  
    return [x, y]
  }

  const bezierCommand = (point, i, a) => {  // start control point
    const [cpsX, cpsY] = controlPoint(a[i - 1], a[i - 2], point)  // end control point
    const [cpeX, cpeY] = controlPoint(point, a[i - 1], a[i + 1], true)  
    return `C ${cpsX},${cpsY} ${cpeX},${cpeY} ${point[0]},${point[1]}`
  }
</script>

<path d={d}></path>