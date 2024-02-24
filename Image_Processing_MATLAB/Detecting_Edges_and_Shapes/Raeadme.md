#### Detecting Edges
- Edges in images are areas with strong intensity contrasts—a jump in intensity from one pixel to the next
- The edge function
  - You can use the edge function to detect the boundaries of objects in a grayscale or binary image.
  - BW = edge(I,method,threshold)
- Edge detection using the Sobel method
  - By default, edge uses the Sobel method. This method uses intensity gradients to find edges. Regions that have a gradient magnitude, G, above a threshold are identified as edges.
- locate the edges of well-defined objects in a grayscale image by calling the edge function without specifying a threshold.
  - defaultEdges = edge(gs)

- Detecting edges with the Canny method
  - The Canny method detects weak edges if they are connected to a strong edge. Consider the grayscale image on the left with a tall rectangle and three squares. Three edges are marked with blue, red, and yellow lines.
  - The Canny algorithm applies two thresholds to the gradient: a high threshold for strong edges and a low threshold for weak edges. The edge function starts with the strong edges and then grows them to include weak edges that are connected.

-  find the edges of connected objects in the binary image using bwboundaries.
  - boundaries = bwboundaries(BW)
- find out by visualizing the boundaries on top of the original image.
  - visboundaries(boundaries)

#### Detecting Circles
- Start by finding the positions of the coins using the imfindcircles function.
  - [centers,radii] = imfindcircles(I,[rmin rmax])
- To extract the subset of the radii based on the logical index variable, idxd, you can use logical indexing.
  - r(idxd)
  - The centers have two dimensions and you need to extract both.
    - c(idxd,:)

#### Detecting Lines
- The Hough transform starts by searching the binary image for a true value.
- At each true value, the transform identifies straight lines that pass through that position. Each line is defined in terms of an angle, 𝜃, and distance to the upper left corner, 𝜌. These coordinates are incremented in the Hough transform matrix by +1.
- This process is repeated for each true value in the binary mask, creating overlapping sine curves.
- By identifying the peaks in the Hough transform, you can identify the lines that exist in the image.






