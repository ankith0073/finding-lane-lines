#**Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. The project pipeline consisted of the following steps
      1.Read in the Image consisting of 3 channels
      2.Conversion of color image to grayscale
      3.Noise reduction 
      4.Edge detecion to detect edges in the lane
      5.Region of interes definition to extract only the required part of the image
      6.Extract lines from edge detected image within the region of interest
      7.Draw the lines on the original image representing lane lines
      
      The detailed steps are explained below 
      
      1.Assuming the camera is mounted on the car, the image read in looks like below
      [//]: # (Image References)

      [image1]: ./examples/solidWhiteCurve.jpg
      
      2.The image is converter to grayscale from RGB space, after which the image looks as below
      [//]: # (Image References)

      [image1]: ./examples/grayscale.jpg
      
      3.After doing noise using a gaussian filter of size [3,3] the image is as shown below
       [//]: # (Image References)

      [image1]: ./examples/solidWhiteCurve_gaussian.jpg
      
      4.Next the images are passed to an edge detecor, where edge detection is done using Canny edge detection
      The canny edge detector has the following parameters
      low_threshold = 50                                            
      high_threshold = 150
      
      [//]: # (Image References)

      [image1]: ./examples/solidWhiteCurve_canny.jpg
      
      5,6,7].The lines are extracted using hough transform with the following parameters parameters
        rho = 1                                                       
        theta = np.pi / 180                                           
        threshold = 10                                                
        min_line_length = 10                                         
        max_line_gap = 15
        
        The output of the hough transform is overlayed on the original image 
        
        [//]: # (Image References)

        [image1]: ./examples/solidWhiteCurve_output.jpg
        
        As seen in the above image We need a single solid line representing the lanes on either side, So the output points of the hough transform lying on the left side is separated from the points lying on the right side of the image. We fit a line to left set of points and to the right points separately using linear regression.
        
         [//]: # (Image References)

        [image1]: ./examples/2_lines_line_output.jpg
        
        The linear regression output is overlayed on the original image, then the output images look like 
        
        [//]: # (Image References)

        [image1]: ./examples/solidWhiteCurve_liner_regression_output.jpg
        
        The above procedure is done on other images and the results are as shown below
        
        [//]: # (Image References)

        [image1]: ./examples/solidYellowCurve2_liner_regression_output.jpg
        
        [//]: # (Image References)

        [image1]: ./examples/whiteCarLaneSwitch_liner_regression_output.jpg     
      
      
      

![alt text][image1]


###2. The potential shortcomings of the above procesure is 
    1) The parameters have been chosen to be static
    2) There is no compensation for high lighting and low lighting conditions


###3.A possible improvement would be to 
    1) Study suggests that processing when done in HSV space is better than working with RGB space.
    2) HSV space allows to handle dynamic lighting conditions
    

