### Introduction
-  will learn a variety of methods to enhance contrast where you want it, and smooth it out when you don't.

### Adjusting Contrast
- Why do you adjust contrast in an image?
  - Low contrast can make the image less attractive and difficult to see—sometimes so hard to see that you wouldn't even know where to start.
 
- use the imhist function to display a histogram of the pixel intensities of an image.
  - imhist(image)
- imadjust function automatically adjusts intensity values to increase contrast.
  - Iadj = imadjust(I);
- brighten the image using the imlocalbrighten function.
  - imgLight = imlocalbrighten(img);
- To adjust an image I to match the intensity profile of a reference image Iref, use the imhistmatch function.
  - Iadj = imhistmatch(I,Iref);
- The histeq function performs histogram equalization. If no reference histogram is given, histeq uses the uniform distribution.
  - Ieq = histeq(I);
- use the adapthisteq function to perform adaptive histogram equalization.
  - Iadapt = adapthisteq(I);
- extract the data field from the input structure, blockStruct.
  - blockStruct.data
  

### Block Processing
- Block processing allows you to apply an algorithm block-by-block.
- adjust the contrast block-by-block using the blockproc function.
- imBP = blockproc(im,blockSize,@functionName);
  - blockproc processes distinct rectangular blocks one at a time by creating and passing a block struct with information about the block to the block processing function.


### Filtering Noise
- Spatial filtering smooths your image, removing noise and unwanted detail. This helps certain image-processing algorithms produce better results.
- Linear filtering is a type of spatial filtering that replaces each pixel with a weighted sum of the pixels around it. Linear filters look at a neighborhood around a pixel of interest and scale each value. Then these products are added together. This becomes the value of that pixel in the new image.
  - A common filter is the **averaging filter** that replaces each pixel with the average value in the neighborhood.
  - A **disk (pillbox) filter** is a weighted average where pixels close to the pixel of interest are weighted more heavily.
  - The **Sobel filter** emphasizes horizontal edges.
- create a filter using the fspecial function.
  - filt = fspecial("type",filterSize)
- use imfilter to filter an image with a specified filter.
  - imFiltered = imfilter(im,filt);

- use medfilt2 to replace each pixel with the median of the ones around it.
  - imFiltMed = medfilt2(im,filterSize);
- use the wiener2 function with the same syntax as medfilt2
  - imFiltW = wiener2(im,filterSize);


### Quality Metrics

- After processing an image, you may need to evaluate the quality of that processing
- Image acquisition and processing can degrade the quality of an image by adding distortions such as noise, blurring, compression artifacts, etc.
- There are two types of quality metrics depending on the type of image and your application—full-reference and no-reference metrics. The type of image quality metric you use depends on whether or not you have a reference image with no distortion.
- The peak signal-to-noise ratio of an image with respect to a reference can be calculated with the psnr function.
  - peaksnr = psnr(im,ref);
- the structural similarity (SSIM) index can better reflect how well structures (e.g. edges and corners) are preserved. The SSIM index is between 0 and 1, with higher numbers representing better quality.
- ssim function takes the same inputs as the psnr function.
  - ssimMetric = ssim(im,ref);

- average linear, median, and Wiener filters
  - Images filtered using average linear, median, and Wiener filters are saved in variables tumorAvg, tumorMed, and tumorW respectively.
- The Natural Image Quality Evaluator (NIQE) can measure the quality of images with arbitrary distortion with a lower score being better.
- To calculate the NIQE score, use the niqe function.
  - score = niqe(I)
- To calculate the BRISQUE score, use the brisque function.
  - score = brisque(I)
 

### Background Subtraction

- nones(n) => the neighborhood with the filter size
- The imtophat function removes uneven background illumination when the background is darker than the foreground.
  - I2 = imtophat(I, nhood);

- Use imbothat to subtract the image from its bright background.
  - im2 = imbothat(Im, nhood);







