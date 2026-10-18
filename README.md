# Delaunay Mesh

An educational, interactive explorer for Delaunay triangulations and circumcircles.

A Delaunay mesh joins a set of points into triangles so that no point lies inside any
triangle's circumcircle: the circle that passes through all three of its corners. This
page lets you place your own points, build the mesh, and inspect any triangle to see
that property for yourself.

This is a teaching aid, not a geometry library. The code favours readability over
speed and numerical robustness.

## Using it

1. Click or tap to place points.
2. Press **Confirm** to build the Delaunay mesh (at least three points, not all in a line).
   The build plays back step by step, starting from the super-triangle. Each point is
   added in four steps: the new point arrives, the triangles whose circumcircles contain
   it are found, they are cut out to leave a hole, and the hole is filled by joining the
   new point to its rim. The clean-up then removes the super-triangle and, if that leaves
   gaps along the edge, patches them.
   - **Play / Pause**, and **Back** / **Next** to step one at a time (or ← / → and Space).
   - The speed button cycles through 0.5×, 1×, 2×, 4× and 8× (1× is one step per second).
   - **Skip** jumps to the finished mesh. **Replay** plays the build again.
3. Tap inside any triangle to highlight it and draw:
   - its circumcircle,
   - the circumcentre,
   - the three perpendicular bisectors of its sides, which meet at the circumcentre.
4. Press **Reset** to start again.

Zoom with the **+** / **−** buttons, the mouse wheel, or a two-finger pinch. Click-and-drag
or touch-and-drag to pan.

## How it works

- The mesh is built with the [Bowyer-Watson algorithm](https://en.wikipedia.org/wiki/Bowyer%E2%80%93Watson_algorithm):
  start from a "super-triangle" just big enough to enclose the points, insert points one
  at a time, remove every triangle whose circumcircle contains the new point, and
  re-triangulate the resulting hole.
- Simply deleting the super-triangle's triangles at the end is not enough: a true Delaunay
  triangle along the hull is never built if its circumcircle contains a super-triangle
  corner, which leaves notches in the mesh. A bigger super-triangle only makes this rarer.
  Instead, each corner is removed in turn and the gap it leaves is refilled with Delaunay
  triangles, so the result is correct for any enclosing super-triangle.
- For the replay, `delaunay()` optionally records each insertion into a trace. The
  player then just draws one recorded step at a time, so the algorithm itself stays
  a plain loop.
- Finding the tapped triangle is a straightforward point-in-triangle test against every
  triangle in the mesh.

## Running it

It is a single self-contained `index.html` with no dependencies, build step or server.
Open it in a browser, or serve the directory with any static file server.
