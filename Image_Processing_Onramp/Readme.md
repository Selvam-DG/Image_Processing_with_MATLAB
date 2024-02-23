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
  - Apply a filter F to an image I by using the imfilter function.
    - Ifltr = imfilter(I,F);
    - To adjust this behavior, use the "replicate" option.Ifltr = imfilter(I,F,"replicate");

- Isolate the Image Background
  - Receipt images that have a busy background are more difficult to classify because artifacts pollute the row sum. To mitigate this issue, you can isolate the background and then remove it by subtraction.
  - In a receipt image, the background is anything that is not text, so isolating the background can be interpreted as removing the text. One way to remove text from an image is to use morphological operations.
  - can create a structuring element by using the strel function.
    - SE = strel("diamond",5) = > defines SE as a diamond-shaped structuring element with a radius of 5 pixels
  - To perform a closing operation on an image I with structuring element SE, use the imclose function.
    - Iclosed = imclose(I,SE);
  -  NOT operator (~). 


- Enhancing Patterns
  - Morphological operations are useful not only for removing features from an image but also for augmenting features. You can use morphology to enhance the text in the binary image and improve the row sum signal.
  - Morphological opening expands the dark text regions, while closing diminishes them. Increasing the size of the structuring element increases these effects.
  - can create a rectangular structuring element using strel with a size array in the format [height width].
    - SE = strel("rectangle",[10 20]);
  - imopen with a wide rectangular structuring element turns lines of text into black horizontal stripes, which augments the valleys in the row sum signal.
    - Iopened = imopen(I,SE);


### Batch Processing with Iamge DataStore

- The imageDatastore function creates an image datastore for all the image files in a folder but won't load them into memory until they are requested.
  - ds = imageDatastore("localFolder")
- we can access the datastore's properties by using a period (.)
  - ds.Folders

- The readimage function loads the nth image from an image datastore into the MATLAB workspace.
  - img = readimage(ds,n);


# Overall Algorithm
function isReceipt = classifyImage(I)
    % This function processes an image and
    % classifies the image as receipt or non-receipt
    
    % Processing
    gs = im2gray(I);
    gs = imadjust(gs);
    
    mask = fspecial("average",3);
    gsSmooth = imfilter(gs,mask,"replicate");
    
    SE = strel("disk",8);  
    Ibg = imclose(gsSmooth, SE);
    Ibgsub =  Ibg - gsSmooth;
    Ibw = ~imbinarize(Ibgsub);
    
    SE = strel("rectangle",[3 25]);
    stripes = imopen(Ibw, SE);
    
    signal = sum(stripes,2);  

    % Classification
    minIndices = islocalmin(signal,"MinProminence",70,"ProminenceWindow",25); 
    nMin = nnz(minIndices);
    isReceipt = nMin >= 9;
    
end














