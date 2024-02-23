-  use the imfinfo function to extract image file information.
  - info = imfinfo("filename.png")
- To extract a field from a structure, use dot notation.
  - struct.FieldName
  - for example : taken2011 = imfinfo("bearGlacier2011.png").CreationTime or d1 = datetime(taken1980)
 - Three different types of Images in MATLAB
   1. GrayScale
      - A grayscale image is stored as a 2-dimensional array, or matrix. Each element of the matrix represents a pixel intensity, which can be any integer from 0 to 255.
   2. RGB true color image
      - An RGB, or truecolor, image is a color image. Each pixel is defined by red, green, and blue intensity values that can each be any integer from 0 to 255.
      - RGB images are stored in a 3-dimensional array. The first plane contains the red intensities, and the second and third contain the green and blue respectively. 

   5. Indexed image
      - Indexed images use a discrete, predefined set of colors. Since indexed images use fewer colors than RGB images, this can reduce the amount of space required to store an image.
      - There are two elements that define an indexed image with m colors:
        - a matrix of indices that range form 0 to m-1 and
        - a colormap that defines what the indices mean.


- while import an indexed image, you need to import the map as well.
  -  [I,map] = imread("filename.png");
  -  imshow(I,map) => to show the indexed image

- convert from an indexed image to a RGB or grayscale image with ind2rgb or  ind2gray.
  - rgb = ind2rgb(I,map);
  - gs = ind2gray(I,map);

- imwrite(I,filename) => save RGB and grayscale images with imwrite
- imwrite(I,map,filename) => save indexed images with imwrite by passing the colormap in addition to the image and filename.


##### Rescaling Images
- After performing calculations on an image of data type double, some intensities might be outside of the range 0 to 1. You can scale the intensities back to the required range with rescale and imadjust.
  - rescale: Scales all pixels to between 0 and 1.
  - imadjust: Scales all pixels to between 0 and 1 while saturating the bottom and top 1%
- Pass [] as a second input to imshow to display an image using the full display range.
  - imshow(I,[])
- use im2double to convert an image to data type double. This also scales the image so that the values are between 0 and 1.
  - imDbl = im2double(im);


##### Binary images 
- Binary images are black and white images. They are typically stored as a logical array where 0 indicates a black pixel and 1 indicates a white pixel.
- A common type of binary image is a mask, or segmentation. A mask separates another image into two regions: white foreground and black background.


- use imoverlay to burn a mask onto an image.
  - maskedImage = imoverlay(I,mask);









