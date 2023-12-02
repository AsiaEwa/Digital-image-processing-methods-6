# Digital-image-processing-methods-6

## operations using FFT - Fourier transform

The purpose of the Fourier transform is to decompose a periodic function into a series of periodic functions in such a way that the resulting transform gives an indication of how the individual frequencies contribute to the original function. Discrete values will appear much more often in image processing. For this purpose, it is more appropriate to use the discrete Fourier transform. However, for practical reasons, the fast Fourier transform - FFT will be most often used in image processing.

Recognizing text, especially handwritten text, seems to be quite a challenge. It has long been known that artificial neural networks are used to read handwriting. However, when analyzing the image, we can support computers by properly preparing the material for analysis.
In order to introduce the use of FFT in identifying letters, we will focus on the letter A. In the first step, let's see what the effect on the image after the Fourier transform is.

As you can see, each line introduces a distinct change in the FFT image

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/1b15dabf-8cfb-4cf8-9466-9957b033db0a)

In the next step, we will check how much the shape of the letters affects the FFT image.

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/565b7cf7-1a02-418a-afd3-bab09ac01199)

As the spectrum between different writing styles differs, there are some similarities.

In the next step, let's check what effect the noise of the original image has on the FFT image.

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/e0955b12-f39c-41a7-8833-9ce8f3c3b0e9)

The FFT1.m script checks what the previously prepared letters created in paint look like.

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/d5bef1bd-510c-431b-9e3b-c6b6d183be6b)

Analyzing the above example, you can notice the similarity in the FFT images. There is a similar distribution of lighter lines for the same letter. The light lines for the third example (letters in the written version) are the least visible. The second FFT image shows additional dark lines at a 45-degree angle.
In the example given, the star is always clear, but the noise brightens the entire image space. The clear image is clear and the star's propagation lines are noticeable. The more noise there is, the more focused the stars are (no lines spreading from the star).

Image ghost: "script1" - load the image 'lena.png'.
  
![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/3c71f6df-f3cb-480c-ac7d-a247b9eab3a2)

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/e18ead6c-8d34-42c5-b5d5-7ed50b671d2a)

The running program loads the image and transforms it into a black and white image, defines the image dimensions and creates x and y matrices based on them. Then it creates an FFT matrix of the black and white image and creates another matrix by shifting the FFT spectrum, calculating its modulus and converting the scale to logarithmic. Then comes the creation of charts and displaying the results of the program.
In the case of geometric images, there is a relationship between the number of lines with higher values and the number of edges in the image. For non-geometric images, many lines can be seen, but there are no clear peaks in the transform values, which makes it difficult to interpret what the image was based on the spectrum.

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/5865a404-a2bf-4e02-97dc-ed61d71b0d63)

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/a78ed4ca-b2b3-41e6-866c-a875c785c8ea)

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/c1593fc4-f456-45f5-82aa-eb12365ae9b1)

the resulting image without using the logarithm function

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/e8595444-35c2-4224-835b-dec9efedc382)

Without changing the scale to logarithmic, it is not possible to observe changes in the image spectrum because all changes are visible in one small point, too large an area is observed.

Implementation of filters in the time and frequency domain
influence of filters in the time and frequency domains.

The image to be processed and masks used to implement filters are loaded in the feed. The loaded image is transformed into a black and white image, then transformed with the FFT function and spectrum shifted. Subsequently, a sub_mask is created based on the entered filter mask. The sub_mask is subjected to an FFT transform. After this, there is a part of the program presenting the results in which the image after the FFT transform is filtered by maske_FFT and the image after such filtering is displayed.

Mask 1:

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/9c352a19-36ac-4987-a7bd-f111c3eda83e)

After a mask similar to a Gaussian filter, the edges of the letter are smoothed and the lines of the letter are thickened.

Mask 2:

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/ba885a33-4eef-4eca-bae4-7c8d1ff5d921)

After the averaging mask, the letter image has blurry edges.
Mask 3:

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/80a6a629-b442-4f04-8228-31405eadaf72)

After applying this filter mask, you can see the background color change to gray, and the letter itself no longer consists of continuous lines. Each line of the letter now consists of an inner line and a line surrounding that line.
2. Test the filter masks from the previous laboratory (masks will be provided by the instructor). Attach the resulting images in the report.

Square filter:

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/b8b4687e-159e-4dee-bef5-54b7d29342cc)

Blurs the edges of the letter lines.
Circular filter:

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/9d50dc68-9cc6-46d4-a844-a60f5c79b360)

The filter blurs the edges of the lines but thickens them.

Interpolation in the frequency domain
Interpolation – a process by which new, previously non-existent pixels are created. The values of the newly created pixels are calculated using one of many methods in such a way that it is best parametrically adjusted to the remaining neighboring values of the transformed image. The quality of the match varies depending on the method used. In this task, the bicubic (Bicubic) technique of image interpolation in the frequency domain will be presented.

Bicubic interpolation uses a mechanism based on determining the FFT spectrum of a special mask and calculating the product of this spectrum with the spectrum of the image to be interpolated. Then, perform the inverse Fourier transform of the calculated product. In the case of bicubic interpolation, the mask takes the form of a special b-spline function.

First, the script creates an image from random pixels and enlarges it 4 times. Then it transforms it to FFT and shifts the spectrum, calculates the modulus and changes the scale to logarithmic. Then a b-sline matrix is created and displayed. Subsequently, this matrix is supplemented with zeros to the dimensions of the processed image and is also displayed. At the end, the results of the program are displayed, including image interpolation. The resulting image has smooth color transitions and has much smaller pixels. The resulting colors are the result of the colors of adjacent pixels. The main shapes have been preserved in the painting

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/38a3e08c-4bee-40f8-8f25-a8444ee2e4d0)

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/1c2eb51d-5555-4a79-bb36-ac96e2a83eca)

The 4B script works very similarly to script 4A, with a slight change in that it loads a ready-made image instead of creating it from random pixels. In this case, you can also see color alignment and blurred edges in the image, but no pixel edges are visible in the resulting image

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/e9ca58c2-017c-4db6-949d-3cacd1760b5f)

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/10fe3b19-1632-4fa5-a141-4f672e377af7)

Dleta_x = 0.2 and delta_y = 0.2

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/751eea1d-fa30-468e-a533-0d7e6390fbb4)

Dleta_x = 5 and delta_y = 5

![image](https://github.com/AsiaEwa/Digital-image-processing-methods-6/assets/101841759/7e995cc2-7733-46a2-9be6-a36d063ac3bf)

It can be seen that the larger the delta_x and delta_y parameters, the less edge blurring and the more the image retains its original form and the less smooth the color transitions between pixels. The smaller the parameters, the more the opposite effect.
