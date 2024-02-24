#### Introduction
#### Texture
#### Texture Filter
-  use spatial filtering to measure texture within a neighborhood. Once you have an image that quantifies texture, you can use intensity-based techniques to segment it.
- Types of Texture Filters:
  - There are three types of texture filters: range filter, standard deviation filter, and entropy filter. Each of them look at a neighborhood around each pixel and replaces that pixel with a measure of the texture around it.
  - The range filter replaces the center pixel with the range of the neighborhood
  - The standard deviation filter replaces the center pixel with the standard deviation of the intensities in the neighborhood.
  - The entropy filter replaces the center pixel with the entropy of the intensities in the neighborhood. Entropy is a measure of randomness.
 

- Use stdfilt to apply a standard deviation filter to fishGray.
  - The stdfilt function automatically converted the image to a double array for increased precision in the calculation. The standard deviations of values from 0 to 255 are outside of the range 0 to 1, so the entire image was saturated and appears white
- Use rangefilt to apply a range filter to fishGray.
  - J = rangefilt(I) 
- Use entropyfilt to apply an entropy filter to fishGray.
  - J = entropyfilt(I)

- neighbor filters
  - can create nxn neighborhood filter  in diagonal matrix; nhod = ones(n);
  - can create an n-by-n neighborhood with the true function. all elements in the filter are 1
  - nH = true(n);
  - nhod = true(n,m) => this create nxm matrix filter with all elements are 1
  - 
  - 







