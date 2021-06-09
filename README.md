# Lane-Line-Detection-Using-OpenCV
Lane lines are detected from the front camera feed of the car and used to hold the car in the lane. It can be also useful for Cruise Control System.
					                                                                  ABSTRACT

In these times of the technological advancement in all the the sectors, self drive cars are considered to be the technological pinnacle of the transportation. lane detection is a critical component of self-driving cars and autonomous vehicles. It is one of the most important research topics for driving scene understanding. Once lane positions are obtained, the vehicle will know where to go and avoid the risk of running into other lanes or getting off the road. This can prevent the driver/car system from drifting off the driving lane. For vehicles to be able to drive by themselves, they need to understand their surrounding world like human drivers, so they can navigate their way in streets, pause at stop signs and traffic lights, and avoid hitting obstacles such as other cars and pedestrians. Based on the problems encountered in detecting objects by autonomous vehicles an effort has been made to demonstrate lane detection using OpenCV library, Canny and Python programming. The reason and procedure for choosing grayscale instead of colour, detecting edges in an image, selecting region of interest, applying Hough Transform and choosing polar coordinates over Cartesian coordinates has been discussed. 

 
                                                                          INTRODUCTION


Autonomous Driving Car is one of the most disruptive innovations in AI, fuelled by Deep Learning algorithms, they are continuously driving our society forward and creating new opportunities in the mobility sector.  An autonomous car can go anywhere a traditional car can go and does everything that an experienced human driver does, but it’s very essential to train it properly. A lane is part of a roadway (carriageway) that is designated to be used by a single line of vehicles, to control and guide drivers and reduce traffic conflicts. One of the many steps involved during the training of an autonomous driving car is lane detection, which is the preliminary step. One of the prerequisites to have in a self-driving car is the development of an Automatic Lane Detection system using an algorithm. The task that we wish to perform is that of real-time lane detection in a video. There are multiple ways we can perform lane detection. The concepts used are listed below. 

                                                                      PROGRAMMING LANGUAGE
                                                                      
	We used python programming language to code. Python is a general purpose and high-level programming language. We can use Python for developing desktop GUI applications, websites and web applications. The simple syntax rules of the programming language makes it easier for us to keep the code base readable and application maintainable. Python is also used in many advanced fields like data science/analysis, Machine Learning, and Artificial Intelligence.

                                                                    Canny edge detection
                                                                    
	The purpose of edge detection in general is to significantly reduce the amount of data in an image, while preserving the structural properties to be used for further image processing. Canny Edge Detector computes gradient in all directions of our blurred image and traces the edges with large changes in intesity.

                                                                      Region of Interest
                                                                      
	This step is to take into account only the region covered by the road lane. A frame mask is nothing but a NumPy array. When we want to apply a mask to an image, we simply change the pixel values of the desired region in that image to 0, or 255, or any other number. A mask is created here, which is of the same dimension as our road image. Furthermore, bitwise AND operation is performed between each pixel of our canny image and this mask. It ultimately masks the canny image and shows the region of interest traced by the polygonal contour of the mask. It is a pretty simple but effective method of removing unwanted regions and objects from the images. Noise can create false edges, therefore before going further, it’s imperative to perform image smoothening. Gaussian filter is used to perform this process.

                                                                      Hough Line Transform
                                                                      
	Hough Transform is a technique to detect any shape that can be represented mathematically. The Probabilistic Hough Line Transform is used here, which gives output as the extremes of the detected lines. For example, it can detect shapes like rectangles, circles, triangles, or lines. We are interested in detecting lane markings that can be represented as lines. We need to follow this process for all the frames and then stitch the resultant frames into a new video.


                                                                             METHODOLOGY
	
Open CV
	
OpenCV means “Open-Source Computer Vision”, which is a package that has many useful tools for analyzing images.
The project involves detection of lane lines in an image using Python and OpenCV

first import the required libraries:

•	NumPy: It comes by default with anaconda

•	OpenCV: It can be installed in two ways, using anaconda or using pip.
	To install using anaconda, type- “conda install -c conda-forge opencv”, or to install using pip, 	type-
	“pip install opencv-python” into your command line

In order to convert the image to grayscale we will first make a copy of the original image using Numpy.


                                                                    GAUSSIAN BLUR

Each of the pixels for a grayscale image is described by a single number that describes the brightness of the pixel. In order to
smoothen an image, the typical answer would be to modify the value of a pixel with the average value of the pixel intensities
around it. Averaging out the pixels to reduce the noise will be done by a kernel. This kernel of normally distributed
numbers(np.array([[1,2,3],[4,5,6],[7,8,9]]) is run across our entire image and sets each pixel value equal to the weighted average
of its neighboring pixels, thus smoothening our image. In our case we will apply a 5x5 Gaussian kernel.


                                                               CANNY EDGE DETECTION FUNCTION 

The canny function calculates derivative in both x and y directions, and according to that, 
we can see the changes in intensity value.n edge corresponds to a region in an image where there is a sharp change in the intensity/colour between adjacent pixels in
the image. A strong gradient is a steep change and vice versa is a shallow change. Larger derivatives equal to High intensity(sharp changes), 
Smaller derivatives equal to Low intensity(shallow changes) . So in a way we can say an image is a stack of
matrix with rows and columns of intensities . we are computing the
gradient (which is change in brightness) in all directions. It then traces the strongest gradients with a series of white pixels.

                                                                      REGION OF INTEREST

Our region of interest is in the shape of a polygon.
The dimensions of the image are chosen which will contain the road lanes and mark it as our region of interest or the triangle.
We want to mask everything except this region. Therefore, we first have to specify the coordinates of the polygon and then use it to prepare the frame mask .
Then a mask is created which is same as the dimension of the image which would essentially be an array of all zeros. Now we
fill the triangle dimension in this mask with the intensity of 255 so that our region of interest dimensions are white. Now, we will
do a bitwise AND operation with the canny image and the mask which will result in our final region of interest.
Image after doing a bitwise operation with the canny image and the mask, also called the masked_image.


                                                                        HOUGH TRANSFORM


 we use of hough transform technique that will detect straight lines in the image and thus identify the lane lines.
Straight line is represented by the equation

y = mx + b

The slope of the line is simply a rise over run. If the y intercept and slope is given then the line can be plotted in the Hough
Space as a single dot. There are many possible lines that can pass through this dot each line with different values for m and b.
and even many possible lines that can cross each point individually, each line with different slope and y intercept values.
However , there is one line that is consistent with both points which we can determine that by looking at the point of intersection
enough space because that point of intersection in Hough Space and that point of intersection represents the M and B values of
a line consistent with crossing both the points . First split our Hough space into a grid.e. For every point of intersection in a Hough
Space bin we're going to cast a vote inside of the bin that it belongs to. The bin with maximum number of votes will be our line.To express vertical lines, we will use polar coordinates instead of
cartesian coordinates as the slope of a vertical line is infinity .
