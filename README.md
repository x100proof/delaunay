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
3. Tap inside any triangle to highlight it and draw:
   - its circumcircle,
   - the circumcentre,
   - the three perpendicular bisectors of its sides, which meet at the circumcentre.
4. Press **Reset** to start again.

Zoom with the **+** / **−** buttons, the mouse wheel, or a two-finger pinch. Click-and-drag
or touch-and-drag to pan.

## How it works

- The mesh is built with the [Bowyer-Watson algorithm](https://en.wikipedia.org/wiki/Bowyer%E2%80%93Watson_algorithm):
  start from a large "super-triangle", insert points one at a time, remove every triangle
  whose circumcircle contains the new point, and re-triangulate the resulting hole.
- Finding the tapped triangle is a straightforward point-in-triangle test against every
  triangle in the mesh.

## Running it

It is a single self-contained `index.html` with no dependencies, build step or server.
Open it in a browser, or serve the directory with any static file server.
