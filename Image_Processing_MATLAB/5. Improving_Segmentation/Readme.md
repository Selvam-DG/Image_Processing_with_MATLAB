#### Introduction
- here are many ways to get a rough segmentation—intensity thresholding, color and texture segmentation, interactively selecting a region of interest (ROI). Often, these initial segmentations are not perfect and require some cleaning.
#### Cleaning Binary Masks
 - start by removing unnecessary foreground noise from the mask.
 - You can start by removing unnecessary foreground noise from the mask.Then clear extraneous foreground from the borders.
 - Then clear extraneous foreground from the borders.Next, fill holes in the segmentation.
 - emove these pieces of unwanted foreground with a morphological opening operation.
 - also need to fill areas of your mask with a morphological closing operation.

- To fill in holes in a segmentation, you can use the imfill function.
  - BW2 = imfill(BW,"holes");

- can remove small areas of foreground (white regions) with bwareaopen.
  - BW2 = bwareaopen(BW,n);
- **Erosion and Dilation**
  - The processes of replacing each pixel with a local minimum or maximum are called erosion and dilation respectively.
  - erode an image with the imerode function.
    - I2 = imerode(I,SE)
  - dilate an image with the imdilate function.
    - I2 = imdilate(I,SE)
- Opening
  - Opening is erosion followed by dilation using the same structuring element for both operations. The erosion removes stray areas of foreground, and the following dilation restores what's left to its original size. The effect is that small areas of bright foreground are removed.
- Closing
  - Closing is dilation followed by erosion using the same structuring element for both operations. The dilation enlarges the foreground, closing any holes or alcoves. The following erosion restores the components to the original scale. The effect is that small areas of dark background are now included in the foreground.

- create a neighborhood, or structuring element, using the strel function by specifying a shape and size.
  - SE = strel("disk",r);
- A closing operation emphasizes bright spots. In a binary image, that means foreground is emphasized. It can be used to fill out indentations in a segmentation.
  - BW2 = imclose(BW,SE);
- perform opening operations with imopen.
  - BW2 = imopen(BW,SE);
- remove foreground touching the border with imclearborder.
  - BW2 = imclearborder(BW);




#### Growing Segmentations with Active Conours
- Sometimes you may have a starting mask, called a seed, that you want to grow to fill out an entire region
- Active contours is an iterative technique that automatically grows the edges of foreground to fill out a region based on the original image.

- grow a segmentation from an initial seed using active contours.
  - BW2 = activecontour(im,BWseed);

#### Growing Segmentations with the Fast Marching Method

- To apply active contours, you need an initial mask that approximates the location and shape of foreground objects; for example, you can draw a region of interest with roipoly
- Fast Marching Method
  - To apply the fast marching method, you need two things: an initial mask, or seed, and a weight array.
- calculate a weight array of a grayscale image that is bright in areas of low change (e.g. object centers) and dark where there is a lot of change (e.g. edges) with the gradientweight function.
  - wts = gradientweight(gs);
  - The "RolloffFactor" name-value pair controls how fast the weights fall as a function of gradient. Increasing it will increase the sensitivity to the gradient.

- Apply the Fast Marching Method using the imsegfmm function.
  - BW2 = imsegfmm(wts,BW,thresh);


#### Image Segmentation App
- in control window, type imagesegmentor app to open the window
- The Image Segmenter App can be used to segment an image interactively or improve an existing segmentation. This is especially helpful if it isn't clear which techniques will work best.








