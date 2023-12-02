# Digital-image-processing-methods-6

# Digital-image-processing-methods-5-Public
## operations using FFT - Fourier transform

The purpose of the Fourier transform is to decompose a periodic function into a series of periodic functions in such a way that the resulting transform gives an indication of how the individual frequencies contribute to the original function. Discrete values will appear much more often in image processing. For this purpose, it is more appropriate to use the discrete Fourier transform. However, for practical reasons, the fast Fourier transform - FFT will be most often used in image processing.

Recognizing text, especially handwritten text, seems to be quite a challenge. It has long been known that artificial neural networks are used to read handwriting. However, when analyzing the image, we can support computers by properly preparing the material for analysis.
In order to introduce the use of FFT in identifying letters, we will focus on the letter A. In the first step, let's see what the effect on the image after the Fourier transform is

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/4a914151-0d8b-4ad7-a929-549c9d5cb2cf)

As you can see, each line introduces a distinct change in the FFT image

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/c08373fa-f143-4a9a-a45d-949fa4f5bf48)

In the next step, we will check how much the shape of the letters affects the FFT image.

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/43cb52be-64e8-4d8e-a8ca-6b5188ba9243)

As the spectrum between different writing styles differs, there are some similarities.

In the next step, let's check what effect the noise of the original image has on the FFT image.

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/6ab7287d-65d7-4a2f-a6e0-8b77f4ea794e)

The FFT1.m script checks what the previously prepared letters created in paint look like.

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/735036bc-68b8-4d91-aec9-27f7dc871ca9)

Analyzing the above example, you can notice the similarity in the FFT images. There is a similar distribution of lighter lines for the same letter. The light lines for the third example (letters in the written version) are the least visible. The second FFT image shows additional dark lines at a 45-degree angle.
In the example given, the star is always clear, but the noise brightens the entire image space. The clear image is clear and the star's propagation lines are noticeable. The more noise there is, the more focused the stars are (no lines spreading from the star).

Image ghost: "script1" - load the image 'lena.png'.
  
![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/f41ad22a-cf9a-4659-8621-5eebf328dd04)

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/3b24df15-a66d-4bb8-9ceb-90b5ade4e217)

The running program loads the image and transforms it into a black and white image, defines the image dimensions and creates x and y matrices based on them. Then it creates an FFT matrix of the black and white image and creates another matrix by shifting the FFT spectrum, calculating its modulus and converting the scale to logarithmic. Then comes the creation of charts and displaying the results of the program.
In the case of geometric images, there is a relationship between the number of lines with higher values and the number of edges in the image. For non-geometric images, many lines can be seen, but there are no clear peaks in the transform values, which makes it difficult to interpret what the image was based on the spectrum.

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/b975f4f3-73a9-465a-8ab1-9de3564c1f1f)

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/19162c0a-5289-4444-a735-ee6d0e17c633)

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/81ccbc45-88b0-4c5f-92a5-ca797ab4dd1f)

the resulting image without using the logarithm function

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/4f814d65-47a9-4f39-ba7e-9e9d045a4713)

Without changing the scale to logarithmic, it is not possible to observe changes in the image spectrum because all changes are visible in one small point, too large an area is observed.

Implementation of filters in the time and frequency domain
influence of filters in the time and frequency domains.

The image to be processed and masks used to implement filters are loaded in the feed. The loaded image is transformed into a black and white image, then transformed with the FFT function and spectrum shifted. Subsequently, a sub_mask is created based on the entered filter mask. The sub_mask is subjected to an FFT transform. After this, there is a part of the program presenting the results in which the image after the FFT transform is filtered by maske_FFT and the image after such filtering is displayed.

Mask 1:

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/7d45dbfa-9c46-4791-aa1c-3f6863500c02)

After a mask similar to a Gaussian filter, the edges of the letter are smoothed and the lines of the letter are thickened.

Mask 2:

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/92c5f734-6e06-42cc-91f4-b36fc318a954)

After the averaging mask, the letter image has blurry edges.
Mask 3:

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/df1ae41a-ea01-4951-8194-1dce8455a708)

After applying this filter mask, you can see the background color change to gray, and the letter itself no longer consists of continuous lines. Each line of the letter now consists of an inner line and a line surrounding that line.
2. Test the filter masks from the previous laboratory (masks will be provided by the instructor). Attach the resulting images in the report.

Square filter:

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/261be141-c694-49e8-8a9d-a8d68c8c0235)

Blurs the edges of the letter lines.
Circular filter:

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/ceb71c25-0e6d-4a62-be5a-2efabd1df7c5)

The filter blurs the edges of the lines but thickens them.

Interpolation in the frequency domain
Interpolation – a process by which new, previously non-existent pixels are created. The values of the newly created pixels are calculated using one of many methods in such a way that it is best parametrically adjusted to the remaining neighboring values of the transformed image. The quality of the match varies depending on the method used. In this task, the bicubic (Bicubic) technique of image interpolation in the frequency domain will be presented.

Bicubic interpolation uses a mechanism based on determining the FFT spectrum of a special mask and calculating the product of this spectrum with the spectrum of the image to be interpolated. Then, perform the inverse Fourier transform of the calculated product. In the case of bicubic interpolation, the mask takes the form of a special b-spline function.

First, the script creates an image from random pixels and enlarges it 4 times. Then it transforms it to FFT and shifts the spectrum, calculates the modulus and changes the scale to logarithmic. Then a b-sline matrix is created and displayed. Subsequently, this matrix is supplemented with zeros to the dimensions of the processed image and is also displayed. At the end, the results of the program are displayed, including image interpolation. The resulting image has smooth color transitions and has much smaller pixels. The resulting colors are the result of the colors of adjacent pixels. The main shapes have been preserved in the painting

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/b2af458d-cfca-4a1f-809a-6de3f94a46c4)

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/fb834d8c-0dc7-407a-928d-0bf9176429c4)

The 4B script works very similarly to script 4A, with a slight change in that it loads a ready-made image instead of creating it from random pixels. In this case, you can also see color alignment and blurred edges in the image, but no pixel edges are visible in the resulting image

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/bd4c88ae-607f-4c62-b960-5d951892074d)

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/33e2b898-50a2-41e0-922f-5e7dc729e44c)

Dleta_x = 0.2 and delta_y = 0.2

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/0314c2c5-86f6-4ca0-865a-b109f07909c7)

Dleta_x = 5 and delta_y = 5

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/9252e82c-d7d7-4ae7-a08b-a206071e2521)

It can be seen that the larger the delta_x and delta_y parameters, the less edge blurring and the more the image retains its original form and the less smooth the color transitions between pixels. The smaller the parameters, the more the opposite effect.
