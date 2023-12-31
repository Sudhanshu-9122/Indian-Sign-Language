# INDIAN-SIGN-LANGUAGE-DETECTION
## INTRODUCTION
Sign Languages are a set of languages that use predefined actions and movements to convey a message. These languages are primarily developed to aid deaf and other verbally challenged people. They use a simultaneous and precise combination of movement of hands, orientation of hands, hand shapes etc. Different regions have different sign languages. We focus on Indian Sign language numbers using both hands in this project.
The proposed algorithm is applicable for only static hand gestures. The algorithm does not use any database and compare with it, instead it uses a simple logic which make the system fast hence can be used for real time application.


### 1. APPROACH:
The code uses contour detection for solving the problem statement. Contours are basically the borders of any shape, we can use apply them to solve such problems. It is done by using “cv2.findContours” function. Another application of convex hull is used which encloses the figure in a closed convex polygon with minimum area. The code has an excessive use of angles made by the sides of this generated polygon with the X-axis. The X-axis is considered as the top edge of the image. Different signs lead to different combinations of angles by which we can identify them.


### 2. METHOD:
* First of all the mask is made to just extract the hand and avoiding other things in the background. The mask is applied to each frame to display the hand. 
* The contours are fetched from the binary image by dilating to remove any noise occurring in the palm region followed by canny edge detection. Maximum contour area was calculated and then convex hull was found.
*  Now as mentioned above we need the angle of the sides of this polygon. So basically we need the finger tips which has to be the vertex of the polygon.
* So as we have the hull array we store those vertex coordinates in a 2-D list.
* After storing the values we iterate over the array to calculate the angle, by test runs an range is set for the angles to be considered as sometimes such points are caught which lie on the palm border i.e the lower region of hand.
* The number of permitted angles are counted and stored as a finger. But the number of fingers would be one more than te fingers variable.
* Conditions for each of the 10 cases are applied to get the results.


### 3. COMPLEXITY:
* The polygon isnt perfect all the time, i.e the total vertices are not at all related to the number of fingers in it. Sometimes their is a cluster of points at a finger tip. 
* To avoid false finger tip counting we make a list of bin values and through the x coordinates of image. The lowest  Y-values of a bin(i.e lowest Y value for a range of X-values) is considered as a finger tip.
* Still it my happen that two points are too close too each other which can mislead us in detecting number of fingers.
*  So a threshold is provided to avoid too very less distances between two points identified as vertices.
* After satisfying the condition of a vertex the angle between two consecutive vertex is calculated as they get arranged in ascending order of X coordinate.
* Simply, corresponding slope (angle) is calculated between the two points.
* However there is a condition in ‘3’ sign where if the third finger is stretched too much then the chronology is hampered as it detects the side point of the hand at the root of the last finger. That case is taken care with another if statement.
* A problem was observed while detecting the ‘4’ and ‘5’ signs as the hull was fluctuating beyond control leading to false values.
* So convexity defects were used where the point farthest to the polygon is searched where the angle is less than 90 as angle between fingers while showing ‘4’ and ‘5’. This method done to work as a helping hand because the main focus was to execute the task mostly by the angle method.
* The 90 degree angle condition is checked with the help of cosine rule and hence we get 3 and 4 defects in the case of 4 and 5 respectively.


### 4. OTHER POINTS:
* As the code’s motto is to detect language for both the hands it needs a picture of hand to be used by user making  a sign of ‘FIVE’.
* The code calculates the angle between the extreme points of the extreme point in the horizontal direction and if it is greater then zero then the frame is flipped as the condition feeded to the code works for left hand.
* However the results are not that perfect because of the instability of the hull, but each sign is detected correctly while executing.

Contributers:
1. [Prathmesh Ringe](https://github.com/PSR794)
2. [Moskhoda Barhate](https://github.com/mokshada14)
3. [Himanshu Mahajan](https://github.com/vondar)
4. [Siddharth Singh](https://github.com/SIDDXSingh/)
