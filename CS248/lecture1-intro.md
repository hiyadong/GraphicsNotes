## Foundations of Computer Graphics

1. Science and Mathematics

Physics of light, color, optics

Math of curves, surfaces, geometry, perspective

Sampling, signal processing

2. Systems

Parallel, heterogenerous processing

Graphics-specific programming systems

Input/output devices

3. Art and psychology

Perception: color, stereo, motion, image quality...

Art and design: composition, form, lighting


## An Example: how to draw a cube

two questions:

### 1. how do we describe the cube?

8 vertices. 

### 2. how do we visualize this cube?

#### step 1: how to display 3d object to a 2d flat image?

think back history: how do we achieved this with a pinhole camera?

by using a simplified pinhole camera model we can project any 3d object into a 2d plane.

in our cube example, the 8 vertices of the cube can be projected to a new vertex.

#### step 2: how do we draw lines on a computer?

a raster display can be represented as a 2D grid of pixels. 

each pixel can take on a unique color value.

we need a way to convert a continuous object to a discrete representation on the 2d grid.

modern GPU uses a diamond rule to choose if a pixel gets light up or not.

each "pixel square" has an associated diamond inside it, if the line passes this diamond, then the pixel is on.

##### issues:
1. how about the thickness of the line? what happens when a line passes multiple "diamonds"?
2. complexity O(n<sup>2</sup>) pixels in image. we need find a better way than check every single pixel in the image.

**seek algorithm that does work proportional to number of pixels painted when drawing the line**

##### common approaches

bresenham algorithm

first consider an easy special case:

a "shallow" line from bottom left to right top.


after solve the line drawing issue.

**we also need to solve surface, motion, materials, lights, and cameras to render a more realistic picture.**


#### step 3: how to draw a surface?

we can use **triangle** to represent any surface. 

why triangle?

1. can break up other polygons into triangles

2. allow programs to optimize one implementation

3. easy to compute (interpolation, intersect....)

just like the problem we encountered with line drawing. 

the first problem we need to solve is:  how to test if a pixel is covered by a triangle.

approach: point sampling

for each cell (x, y) in 2d grid:
    center = (x + 0.5, y + 0.5)
    if inside(tri, x, y):
        shade(x, y)


how about sample point covered by 2 triangles and on the same shared edge of those both triangles.

OpenGL/Direct3D edge rules:

when edge falls directly on a screen sample point, the sample is classified as within triangle if the edge is a top edge or left edge.

top edge: horizontal edge that is above all other edges

left edge: an edge that is not exactly horizontal and is on the left side of the triangle. (a triangle can have one or two left edges)

optimizition: tiled triangle traversal

all modern gpus have special-purpose hardware for efficiently performing point-in-triangle tests


#### step 4: sampling artifacts

convert a continuous function to a discrete one cause "jaggies". this is one of the common sampling artifacts in computer graphics.

other example:

wagon wheel effect -> undersampling in time

moire -> undersampling images.

the reason:

signals changing faster than the sample rate. sample too sparsely.

solution: 
supersampling:

sample multiple points on the pixel grid and average the sum.

there are other samplingi artifacts 


## Starting out

1. have a broad overview of major topics and techniques in computer graphics.

geometry, rendering, animation, imaging.

2. learn by implementting

fundamental data structures and algorithms that are resued across all areas of graphics.