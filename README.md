# Photo-filters-OpenCV

# Part 1: Photo effects

I got 7 filters for this part:

(a) Brightness and Contrast filter
The algorithm I used to improve (also could decrease) photo’s contrast and brightness is shown below: 

g(i,j)=αxf(i,j)+β

g(i,j) is the original pixel, and f(i,j) is the pixel after the transform. The alpha value would change the contrast of photos, make photos clearer and more colorful, and the beta value would make the photo brighter. This filter could be used on dull photos.

(b) Solarization filter
Solarization is a process used in Photography to describe the effect of tone reversal observed in cases of extreme overexposure of the photographic film in the camera. It is a darkroom technique to convert any photograph to look graphic or surrealistic. The solarization filter invert all pixel values above a threshold, here we chose 128 as the threshold.

(c) Invert filter
In the past, people used film camera to take photos, and the images on films are reversed. This reversed order occurs because the extremely light-sensitive chemicals a camera film must use to capture an image quickly enough for ordinary picture-taking are darkened, rather than bleached, by exposure to light and subsequent photographic processing. This invert filter would invert all of the pixel values and make photos looks like traditional motion picture film rolls in theaters. If you develop the invert film, you will get a normal look photo.

(d) Sepia Filter
Sepia is one of the most commonly used filters in image editing. Sepia adds a warm brown effect to photos, makes the photos looks vintage, calm and nostalgic. And It has a standardized matrix that can be used as the default as shown below:

R = 0.393r + 0.769g + 0.189b G = 0.349r + 0.686g + 0.168b B = 0.272r + 0.534g + 0.131b

The lower r, g, b are the original pixel, and the capital R, G, B are pixel after filter transform.

(e) Comic filter
The comic filter looks similar to the greyscale filter, but the comic filter increases the light and dark contrast of photos, reminds me the comic books when I was young. The algorism is shown below:

R = abs(b-g+b+r)*g/256 
G = abs(b-g+b+r)*r/256
B = abs(g-b+g+r)*r/256
gray = (R+G+B)/3
R = gray + 10
G = gray + 10
B = gray

(f) Castingfilter
The casting filter imitates industrial steel casting, which adds a burning effect to photos, everything would looks like burning or in the hell. The algorism is shown below:

R = r*128/(g+b+1) G = g*128/(r+b+1) B = b*128/(g+r+1)\

(g) Frozen filter
The frozen filter adds a cold effect on photos, and photos would look like they were frozen, have a sense of winter and coldness. The algorism is shown below:

R = abs(r-g-b)*3/2 G = abs(g-b-r)*3/2 B = abs(b-g-r)*3/2

And these 7 filters were applied on these photos:

![1](https://github.com/Weiwei-Wan/Photo-filters-OpenCV/assets/74362292/e72da86a-fb0c-4d40-ba11-ebef7424ded2)

![2](https://github.com/Weiwei-Wan/Photo-filters-OpenCV/assets/74362292/18bf8e94-7047-48cd-813c-083bdf270b9a)

![3](https://github.com/Weiwei-Wan/Photo-filters-OpenCV/assets/74362292/117119a9-c027-4a3e-9638-479afddf106f)


# Part 2: Sharpening, blur, and noise removal 

(a) find edge
Edge detection is used to identify the edges of objects or regions within an image. Edges are characterized by sudden changes in pixel intensity or a sharp difference and change in pixel values. Here the kernel below was used to convolve with this photo.
[[-1, -1, -1],
 [-1, 8, -1], 
 [-1, -1, -1],]
And the edge detection filter was applied:

![4](https://github.com/Weiwei-Wan/Photo-filters-OpenCV/assets/74362292/9a8162d1-a70d-4fab-8486-a90637b80f5d)

(b) sharpen
Image sharpening is an effect applied to digital images to give them a sharper appearance and enhance the definition of edges in an image. This filter would compensate the outline and enhance the edge of dull images who have poor edges, then the images would become clear.
This filter improves the contrast between the edge of the feature and the surrounding pixels, so it is also called edge enhancement. The level of sharpening depends on the type of kernel we use. We have a lot of freedom to customize the kernel here, and each kernel will give you a different kind of sharpening. To just sharpen an image, I used a kernel like this:
[[0, -1, 0],
[-1, 5, -1], 
[0, -1, 0],]
And the sharpening filter was applied:

![5](https://github.com/Weiwei-Wan/Photo-filters-OpenCV/assets/74362292/c810599a-864f-4bf0-b3df-d45716a085a1)

(c) box blur
The box blur filter is done by convolving the image with a normalized box filter. It simply takes the average of all the pixels under kernel area and replaces the central element with this average. We should specify the width and height of kernel before the convolution, for example a 3x3 normalized box filter would look like this:
[[1, 1, 1], 
[1, 1, 1], 
[1, 1, 1],]/9

(d) Gaussian blur
In image processing, a Gaussian blur is the result of blurring an image by a Gaussian function, could reduce the image's high-frequency components, thus it’s a low-pass filter, could reduce image noise and reduce detail. In this approach, instead of a box filter consisting of equal filter coefficients, a Gaussian kernel is used. This Gaussian blur filter is a type of image-blurring filter that uses a Gaussian function (which also expresses the normal distribution in statistics) for calculating the transformation to apply to each pixel in the image. 

(e) median blur
The median blur algorithm computes the median of all the pixels under the kernel window and the central pixel is replaced with this median value. This is highly effective in removing salt-and-pepper noise. One interesting thing to note is that, in the Gaussian and box filters, the filtered value for the central element can be a value which may not exist in the original image. However this is not the case in median filtering, since the central element is always replaced by some pixel value in the image. This reduces the noise effectively.

(f) bilateralblur
The bilateral filter is used for smoothening images and reducing noise, while preserving edges. It also uses a Gaussian filter in the space domain, and both of the space factor and pixel value factor are considered. If a neighbor pixel who exhibited large intensity variation compared to the central pixel, would not be included for blurring. While other blur convolutions (e.g. Gaussian blur only consider space factor but not the pixels’ value and whether the pixel lies on an edge or not,) often result in a loss of important edge information, since they blur out everything, irrespective of it being noise or an edge.

(g) binomial blur
The binomial blur is similar to Gaussian blur but more simple and faster. Binomial filters form a compact rapid approximation of the (discretized) Gaussian kernel.
Here I applied these 5 filters on below photo. We can see from the first image, the bilateral blur could preserve the edge's shape (e.g. the cup and flower), perform better than other filters, the 3rd image could also demonstrated it. And the 2nd image has many salt-and-pepper noises, in this situation, the median blur filter has highest efficiency on removing it. The box blur blurred everything, and the Gaussian blur perform better than the box blur on edge preservation.

![6](https://github.com/Weiwei-Wan/Photo-filters-OpenCV/assets/74362292/ba2a97ca-4cae-4b54-86b4-1ceaab70d4e2)

# Part 3: High-quality image resampling 

(a) Nearest Neighbour Interpolation
Nearest neighbour interpolation is the simplest approach to interpolation. Rather than calculate an average value by some weighting criteria or generate an intermediate value based on complicated rules, this method simply determines the “nearest” neighbouring pixel, and assumes the intensity value of it.
After minifying 2 fold of the image size 3 times then magnify 2 fold of the image size 3 times, it’s oblivious too many sawtooth generated both in the synthetic and natural images. The major drawback of this algorithm is that, despite its speed and simplicity, it tends to generate images with poor quality and blocky.

![7](https://github.com/Weiwei-Wan/Photo-filters-OpenCV/assets/74362292/70d5661e-67dd-4c2e-b0e9-966276f3eed9)

(b) Bilinear Interpolation
Bilinear interpolation is performed using linear interpolation first in one direction, and then again in the other direction. A weighted average of the pixel value of the four surrounding pixels is computed and applied. This process is repeated for each pixel then forming the resized image. The closer an input pixel is to the output pixel, the higher the influence of its value is on the output. This means that the output value could be different than the nearest input, but is always within the same range of values as the input. Since the values would change. And this algorithm generated less sawtooth and blocky area compared to the nearest neighbour interpolation, but a little slower.

![8](https://github.com/Weiwei-Wan/Photo-filters-OpenCV/assets/74362292/81589aee-b50f-4f54-b5ce-6e3fa9789570)

(c) Bicubic Interpolation
Bicubic Convolution looks at the 16 nearest pixels (4×4) to the output and fits a smooth curve through the points to find the value. Not only does this change the values of the input but it could also cause the output value to be outside of the range of input values.

![9](https://github.com/Weiwei-Wan/Photo-filters-OpenCV/assets/74362292/c2ff0094-0238-4ee6-bec0-3e59612c2c08)

(d) Lanczos Interpolation
Lanczos interpolation is used as a low-pass filter to smoothly interpolate images. It maps each sample of the given signal to a translated and scaled copy of the Lanczos kernel, which is a sinc function windowed by the central lobe of a second longer sinc function. 

![10](https://github.com/Weiwei-Wan/Photo-filters-OpenCV/assets/74362292/7ededa0a-7af3-43b9-af92-e4dab426f930)

(e) Gaussian pyramid
The image lowpass pyramid is made by smoothing the image with an appropriate smoothing filter and then subsampling the smoothed image, usually by a factor of 2 along each coordinate direction. The resulting image is then subjected to the same procedure, and the cycle is repeated multiple times. Each cycle of this process results in a smaller image with increased smoothing, but with decreased spatial sampling density. If illustrated graphically, the entire multi-scale representation will look like a pyramid, with the original image on the bottom and each cycle's resulting smaller image stacked one atop the other.
Here the Gaussian pyramid, when down sampling, we can first apply Gaussian blur filter on the image then remove the even rows and columns of the blurred image and get next scale for the pyramid. Repeat the process we would get a pyramid. When up sampling (rebuilt), we can insert rows and columns of zero to the image then apply the Gaussian blur filter on it and we get an upper scale image. However, the sampling make the image lose details, so we can use Laplacian pyramid to save the details (the original image minus the rebuilt one would generate the Laplacian pyramid).
As the images show, the images generated by Gaussian pyramid are blur but no sawtooth and block compared to the previous algorithm, and the original image can recover using Laplacian pyramid.

![11](https://github.com/Weiwei-Wan/Photo-filters-OpenCV/assets/74362292/9b1eee3c-29c5-4580-a541-b5e51b7cb975)
![12](https://github.com/Weiwei-Wan/Photo-filters-OpenCV/assets/74362292/2b25ac0a-9616-4483-ac51-30e6257ae4ce)

