#### Introduction
#### Color Thresholding
- The color of a pixel is defined by the amount of red, green, and blue it contains. An image is a 3-dimensional array with planes containing red, green, and blue intensities.
- You can extract individual color planes by indexing.
  - bluePlane = im(:,:,3);
  - Or, you can extract all of them at once with imsplit.
  - [red,green,blue] = imsplit(im);
#### Color Spaces
- RGB
- HSV
  - The HSV color space breaks image pixels down into Hue, Saturation, and Value. Separating the hue from other qualities of the color allows you to manipulate or segment using any of these
    - Hue is the color's position on the color wheel. The values range from 0 to 1 where both endpoints represent red and values in between represent how far along the the color wheel they are.
    - Saturation ranges from 0 to 1 describes the departure from neutral. Small saturation values are shades of gray and large values represent highly saturated colors (e.g. no white component).
    - Value quantifies brightness and ranges from 0 to 1.
  - The function rgb2hsv converts an image from RGB to the HSV color space.
  - The imsplit function, which you used to extract the color planes from RGB images, can split other color spaces into their respective channels.

[ch1,ch2,ch3] = imsplit(image);
- L* a* b*
  - A representation in the Lab color space has three channels:
    - Luminance is stored in the first plane and contains brightness from black to white.
    - The a* channel is stored in the second plane and contains a measurement of hue from green to red.
    - The b* channel is stored in the third plane and contains a measurement of hue from blue to yellow.
      
- The rgb2lab function converts an image from RGB to Lab.




#### the Color thresholder App
- in commandwindow, type color thresholder t open
- createSBmask.m =>function used as the Color Thresholder App to segment
- use the imoverlay function to burn a mask onto an image.
  - Ioverlay = imoverlay(I,BW,color);



#### Segment Based on a Region of Interest
- Identify the ROI
  - Display the image then call drawpolygon to select the region by marking the corners.
  - imshow(im)
  - roi = drawpolygon;
- Create a mask to isolate the pixels in that region 




