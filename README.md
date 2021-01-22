# **Writeup Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Description of the pipeline

**My pipeline consisted of the following steps:**  
1. First, I converted the images to grayscale, then I surpressed noise and spurious gradients by using a gaussian kernel on the grayscale image.
<figure>
 <img src="./test_images/solidWhiteRight.jpg" width="380" alt="Input image" />
 <figcaption>
 <p style="text-align: center;"> Input image </p> 
 </figcaption>
</figure>
 <p></p> 
<figure>
 <img src="./pipline_images/gray.png" width="380" alt="Grayscale image" />
 <figcaption>
 <p style="text-align: center;"> Grayscale image </p> 
 </figcaption>
</figure>
 <p></p>
2. I then applied Canny edge detection on that gaussian blurred grayscale image. Lower and upper Threshold for the Canny edge detection were chosen in a way, that only the points with a high change in value for the calculated gradients remain. 
<figure>
 <img src="./pipline_images/edges.png" width="380" alt="Image with Canny edge detection" />
 <figcaption>
 <p style="text-align: center;"> Image with Canny edge detection </p> 
 </figcaption>
</figure>
 <p></p>
3. Then I defined a mask for the region of interest. Obviously the region of interest is the road ahead of the vehicle with the left and right lane lines on it. I applied the mask on the edges from the Canny transform, for that I only get the necessary collection of points.
<figure>
 <img src="./pipline_images/masked_image.png" width="380" alt="Masked image" />
 <figcaption>
 <p style="text-align: center;"> Masked image </p> 
 </figcaption>
</figure>
 <p></p>
4. On these points I applied a Hough transformation in order to get lines, these lines were drawn on a black blank image.
<figure>
 <img src="./pipline_images/lines.png" width="380" alt="Masked image with lines form Hough transform" />
 <figcaption>
 <p style="text-align: center;"> Masked image with lines form Hough transform </p> 
 </figcaption>
</figure>
 <p></p>
5. In the next step I added that blank image with the detected line segments together with the initial image.
<figure>
 <img src="./pipline_images/lines_on_img.png" width="380" alt="Input image with detected line segments" />
 <figcaption>
 <p style="text-align: center;"> Input image with detected line segments </p> 
 </figcaption>
</figure>
 <p></p>
6. Then I modfied the draw_lines() function in a way that the multiple segments of single lines are divided into left or right lane segments by using their slope. After that I averaged them and extrapolated a single line for the left and a single line for the right lane line by using cv2s lineFit() function.
<figure>
 <img src="./pipline_images/lane_lines_on_img.png" width="380" alt="Input image with detected lane lines" />
 <figcaption>
 <p style="text-align: center;"> Input image with detected lane lines </p> 
 </figcaption>
</figure>
 <p></p>  
 

**Application on videostream:**  
In a further step I applied that pipline on a video snippet.  
  
**Use of HSV color space:**  
And finally I changed the input from grayscale image to an HSV color space image, in order to get better results on a more challenging video snippet. For that task I used the Value channel of the HSV image with its thresholds between 230 and 255, thus only the pixels with a brightness higher that 230 are chosen as input for the Canny edge detection function. This results in an advanced lane line recognition. 


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen with rainy or snowy weather, a lane line detection based on a grayscale or HSV image could be difficult, when there are no significant differences in brightness between lane lines an their surrounding.

Another shortcoming could be heavy traffic, where the lane lines can rarely be percepted by the camera.

### 3. Suggest possible improvements to your pipeline

Improvements are needed for example for curved or broken lane lines, rain, snow, more traffic, etc. That can be achieved by using machine learning algorithms, that can more efficiently extract the necessary features and its values for more complex environments.
