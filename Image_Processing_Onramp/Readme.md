# Image Processing basic commands

## Load the image in MATLAB:
- imread("filename");
  
- imshow()
- imwrite() - to save image in newfile
-im2gray()
- size(imagefile)
  - to get the size of the image
- imshowpair(image1,image2, "montage");
- imhist(gs)
  - can investigate the contrast in an image by viewing its intensity histogram using the imhist function.
- imadjust ();
  - Increasing image contrast brightens brighter pixels and darkens darker pixels. You can use the imadjust function to adjust the contrast of a grayscale image automatically.
- imlocalbrighten()
  -  to adjust the contrast of a color image

- imtool to open the Image Viewer app and explore the two images 


## Image Segmentation: 
- Intensity Thresholding
  - You can create a binary black-and-white image from a grayscale image by thresholding its intensity values. Values below the cutoff are assigned the value 0, while values above are assigned the value 1.
  - In the example below, a grayscale image was segmented using a threshold of 1/4 the maximum possible intensity of 255.
  - You can use logical operators to threshold the intensity values of a grayscale image, creating a binary image.
    - B = g > thresh;
- imbinarize function, which calculates the "best" threshold for the image.
  - gBinary = imbinarize(g);
  - gBinary = imbinarize(g,"adaptive"); =>  pick the best threshold for that region by passing the "adaptive" option as the second argument to imbinarize
  - BWadapt = imbinarize(gsAdj, "adaptive", "ForegroundPolarity","dark") => we can designate whether the foreground is bright or dark by setting the "ForegroundPolarity" option.

- Identifying Text Patterns
  - You've improved the visibility of the text in a binary image. Now how can you determine if the image is a receipt? The answer lies in the pattern of text in the image.
  - The rows of pixels that contain text have more 0 threshold values, and the rows between lines of text have more 1s. If you sum the values across each row, rows with text have smaller sums than rows without text.

- sum(image,2 )
  - compute the sums across rows of an array by using the sum function operating along the second dimension of the array.





## Preprocessing and Postprocessing to Improve Segmentation
- Segmentation can be improved in two ways: by preprocessing the image before binarizing and by postprocessing the binary image itself.
- You've already done some preprocessing by converting each image to grayscale and adjusting the contrast. In the next few activities, you'll use three additional preprocessing and postprocessing techniques.
- Noise Removal
  - Smooth pixel intensity values to reduce the impact of variation on binarization.
- Background Isolation and Subtraction
  - Isolate and remove the background of an image before binarizing.
- Binary Morphology
  - Emphasize particular patterns or shapes in a binary image


- Filter Noise:
  - fspecial function to create an n-by-n averaging filter.
    - F = fspecial("average",n)
  - pply a filter F to an image I by using the imfilter function.
    - Ifltr = imfilter(I,F);
