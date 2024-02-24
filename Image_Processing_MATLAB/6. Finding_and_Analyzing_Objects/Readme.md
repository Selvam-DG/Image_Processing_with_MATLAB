#### Working with Conncected Components of a Mask
- Segmentation allows you to identify regions of an image based on some quality in the image like color, intensity, or texture. You may need to filter or label the regions to extract practical information.
- Identifying Connected Components
  - A connected component of a mask is a set of foreground (white) pixels that are next to each other.
  - There are different ways pixels can be next to each other. For 2-D applications, pixels are 4-connected if sides touch. Pixels are 8-connected if either the sides or corners touch.
 
- can filter connected components by size using bwpropfilt.
  - compFilt = bwpropfilt(BW,"Area",range); 
- find the connected components of a binary image with bwconncomp.
   - CC = bwconncomp(BW)
- extract a field using dot notation.
  - CC.PixelIdList
- create a label matrix that assigns a different label to each connected component.
  - labels = labelmatrix(CC);

- assign the components a color with label2rgb.
  - rgb = label2rgb(labels)

- The colors appear to have an order from left to right. You can control this, the colormap, and the background color with additional inputs to label2rgb.
  - rgb = label2rgb(labMat,cmap,bg,order);




#### Separating Overlapping Objects with Watershed
- use the bwdist function to calculate the distance matrix that assigns a value to each pixel that is the minimal distance between that pixel and the nearest non-zero pixel.
  - D = bwdist(BW);
 
- take the complement of the grayscale image.
  - I2 = imcomplement(I);
- suppress minima with depth less than h using imhmin.
  - I2 = imhmin(I,h); 
- Apply the watershed algorithm to a grayscale image using the watershed function.
  - ws = watershed(gs);
- Use labeloverlay with the label matrix you created from watershed to view the separated segmentation in context.
  - I2 = labeloverlay(im,labelMat);


#### Measuring shape Properties
- use the regionprops function.
  - stats = regionprops(output,L,props)
- calculate the number of rows of a table with the height function.
  - numRows = height(tbl)
 
- extract columns of data from a table with dot notation.
  - tbl.VarName

- se the bwpropfilt function to keep the n largest or smallest objects when sorted by attrib.
  - BW2 = bwpropfilt(BW,attrib,n,keep);

- regionprops function works on binary images as well as on label matrices. The syntax is the same.
  - stats = regionprops(output,BW,props)
- use imrotate to rotate an image counterclockwise.
  - I2 = imrotate(I,angle);

- display a bounding box over an image by passing it as the position to the rectangle function.
  - rectangle("Position",pos,"Name",Value)









