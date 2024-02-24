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




#### Growing Segmentations with Active Conours
#### Growing Segmentations with the Fast Marching Method
#### Image Segmentation App
