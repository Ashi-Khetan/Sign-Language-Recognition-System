# Sign-to-Speech-conversion
In this project, I have worked with computer vision module named OpenCV and its various features in order extract various information from the webcam video and provide with the sign to speech conversion. This system is useful for the deaf and dumb people to make their communication with the world easier.

Proposed algorithm
Image Processing Algorithm:
Steps to execute image processing for capturing hand gestures are:

⦁	Open camera (cv2):- cv2 is an interface of OpenCV( Open Source computer Vision Libary). OpenCV is a library in Python used to solve problems of computer vision. OpenCV-Python uses Numpy, a highly optimized library with a MATLAB-style syntax for numerical operations. All structures of the OpenCV array are converted from and to Numpy arrays. 
  
⦁	Frame capturing using a rectangle window:- Within the camera video interface, a rectangular area is created within which the background elimination and other operations are performed to process the image.

⦁	Pre- processing (gaussian - blur):- Image pre-processing is done to reduce noise from the image. For this purpose, gaussian blur is used to reduce the details of image by blurring it so as to reduce the noise from it.

⦁	Background /noise elimination( foreground detection):- In this step, we eliminate the background, that is, we separate the background from the foreground to get the foreground object.
   Image at time t: I(u,v,t)
   Background at time t: B(u,v,t)
   The estimated background is taken to be the previous frame , that is, B(u,v,t)=I(u,v,t-1)
   |Current image - Background|>Threshold → Foreground
   |I(u,v,t)-I(u,v,t-1)|>Th→ Foreground

⦁	Conversion of BGR image to HSV (masking)
  The Blue,Green, Red components of an image are related to the intensity of light. It is necessary to separate this luminance with colour components.The dependence of RGB components on the luminance makes the identification of the object difficult. Hence, the Hue,Saturation,Value(HSV) format is used.
The formula to convert an RGB image to HSV is
Red' = Red/255
Green' = Green/255
Blue' = Blue/255
Cmaximum = max(Red', Green', Blue')
Cminimum = min(Red', Green', Blue')
Delta = Cmaximum - Cminimum
Hue=  60o*(((Green’-Blue’)/Delta)mod6) ,  Cmaximum=Red’
60o*(((Blue’-Red’)/Delta)+2),     Cmaximum= Green’
60o*(((Red’-Green’)/Delta)+4),  Cmaximum=Blue’
Saturation= 0 if Cmaximum=0
	       =  (delta/Cmaximum) if not 0
Value= Cmaximum
For example, colour magenta has RGB coordinates, (255,0,255). Using, the above formula , its HSV coordinates are (300o, 100% ,100%)

⦁	Morphological transformation:- Morphological transformation refers to the transformations made in the shape of an image due to certain non-linear operations on it. In our project, we have used two kinds of such transformations:

⦁	Erosion: Erosion is used to erode away the boundaries of the objects in foreground.
Since the pixels of images are represented as matrices in the system so we perform erosion on the matrices. Let  X and Y are two sets in A² where Y is the structuring element of X , erosion of X by Y, denoted by X ⊖ Y is defined as:
 X ⊖ Y = {a | (Y)ₐ ⊆ X} 
This gives set of all points a such that Y, translated by a, is contained in X 

⦁	Dilation: Dilation is reverse of erosion. It increases the boundaries of the objects in foreground.
As pixels of images are represented as matrices ,let  X and Y be sets in A² , dilation of X by Y where Y is the structuring element of X, denoted by X ⊕ Y is defined as:
 X ⊕ Y = {a | (Y’)ₐ ∩ X ≠ ∅} 
Here we reflect Y about the origin, and shift the reflection by a. Dilation is the set of all the  displacements a such that Y and X overlap by at least one element.

⦁	Contours (building up boundary)
Contours form the boundary of an image by linking the edges. In order to find contours of the foreground, we have applied Ramer–Douglas–Peucker algorithm on the boundaries of our foreground. The Ramer-Douglas – Peucker algorithm is an algorithm designed to reduce the number of points in a curve approximated by a number of points. It does so by thinking of a line in a set of points that make up the curve between the first and the last point. It checks which point is farthest from this line in the middle. If the point (and all other intermediate points as follows) is closer than the' epsilon' distance, it removes all these intermediate points. On the other hand, if this outlier point is more distant than epsilon from our imaginary line, the curve is divided into two parts:

⦁	 From the first point to the outlier point

⦁	The outlier and the other points.
             On both resulting curves, the function is recursively called, and the two reduced curve shapes are    put back together. When the recursion is completed, it is possible to generate a new output curve consisting of all and only those points marked as kept.


⦁	Building up a convex hull
Convex Hull is the envelope around a particular set of points to define the boundary. To build this boundary, we first found the minimum and maximum points(minimum- junction between two fingers. Then, connect these two points. The junction between two fingers is always different. Based on the length of the line from the reference line, the finger is identified. Alongside, the number of maximas are counted to know the number of fingers which are unbent. The combination of these two findings gives us the sign that has been shown. 

⦁	This result is finally displayed on the output web cam screen.
