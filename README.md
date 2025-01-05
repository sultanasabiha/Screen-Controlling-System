# **Screen Controlling System using hand gestures** 
  


## **Overview**


The **Hand Gesture-Based Screen Control System** is an innovative project that leverages computer vision and machine learning to create a touch-free interface for controlling computer screens or devices. With the increasing demand for contactless interaction, this project provides a user-friendly solution by translating hand gestures into actionable commands. 

The system utilizes a webcam or camera module to capture real-time hand movements and processes the input using advanced algorithms to recognize predefined gestures. These gestures are then mapped to specific actions, such as cursor movement, clicking, maximizing, minimizing, scrolling, or even switching 

---

## **Technologies Used**
- OpenCV: For image processing and real-time video analysis.
- MediaPipe: For hand tracking and gesture recognition.

<p float="left" align="center">
    <img src="images/Screenshot 2025-01-06 001937.png"/><br>
    MediaPipe Hands Solution Graph   
</p>


- PyAutoGUI: For controlling the mouse and keyboard to automate interactions with other applications. 
- Python: For integrating algorithms and building the application interface.
- Numpy: For efficient numerical computations.

---
## **Installation**
To install the required dependencies and run this project on your local machine:

1. Clone this repository:
   ```bash
   git clone https://github.com/sultanasabiha/Screen-Controlling-System
   cd Screen-Controlling-System
   ```

2. Install the required Python packages:
   ```bash
   pip install -r requirements.txt
   ```
---  
## **Methodology**
Based on the solution provided by MediaPipe our whole project has 5 main component or task based around the landmarks provided by the Hand Solution.

<p float="left" align="center">
    <img src="images/Screenshot 2025-01-05 224242.png"/><br>  
    Landmarks  
</p>
<br>

**TASK-1: Detect hand**
<br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-05 224921.png"/>    
</p>
<br>

**TASK-2: Find coordinates of the landmark**
<br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-05 225006.png"/>    
</p>
<br>

**TASK-3: Detect whether hand is straight or not**
<br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-05 234734.png"/><br>
    Landmarks of interest 
</p>
<br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-05 234749.png" height=45% width=45% hspace="10"/>
    <img src="images/Screenshot 2025-01-05 234804.png" height=45% width=45% hspace="10"/><br>
    Case(1) With respect to Y-axis
</p>
<br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-05 234816.png" height=45% width=45% hspace="10"/>
    <img src="images/Screenshot 2025-01-05 234827.png" height=45% width=45% hspace="10"/><br>
    Case(1) Extended
</p>
<br>

**TASK-4: Detect whether it is left hand or right hand**
<br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-05 234846.png"/><br>
    Landmarks of interest
</p><br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-05 235031.png"/><br>
    Case(1) Hand is Straight
    <img src="images/Screenshot 2025-01-05 235046.png"/><br>
    Case(2) Hand is Not Straight 
</p><br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-05 235103.png"/> <br>   
    Detect whether it is left hand or right hand
</p><br>

**TASK-5: Detect which fingers are up**
<br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-05 235119.png"/><br>
    Landmarks of interest
</p><br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-06 000152.png"/><br>
    Case(1) Hand is straight
</p><br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-06 000206.png"/><br>
    Case(2) Hand is not straight 
</p><br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-06 000225.png"/><br>
    Detect which fingers are up
</p><br>

**SETTING UP THE TRACK AREA**

Track area is the area in which our hand if detected will response to some action like cursor movement, left or right click , switch windows etc.  It is needed because our camera is mapped to the screen, mean the width and height of the camera is mapped to the screen width and height. Now if the hand is in bottom of the camera frame , then it may happen that we are unable to detect the hand thus making the track area smaller than the actual camera frame will always allow us that we are able to capture the hand as well as we are able to travel to bottom of the screen



---

## **Implementation**
**Cursor Movement**
When only the Index finger is UP and all other fingers are down . We track the index finger in the track area then we interpret the index finger to the screen position. But as we are capturing the video and video is a sequence of images we can find the cursor is not stable. Its vibrating  as our hand is not stable at one place. So to fix we need this we need to consider the previous location value and current location value and move to cursor accordingly.

Smooth value: Higher the value, lower the movement(Up to a certain limit)
<br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-06 001013.png" height=45% width=55%/>
</p><br>

**Left Click** 
Left click action is performed when the index finger and middle finger is up and the distance between them is less than 45.
<br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-06 001039.png" height=45% width=55%/>
</p><br>

**Right Click**
Right click action is performed when the index finger and the Pinky finger is up together.
<br><p float="left" align="center">
    <img src="images/Screenshot 2025-01-06 001543.png" height=45% width=55%/>
</p><br>

**Maximize**
Maximize action is performed when all the five finger are up all together
<br><p float="left" align="center">
    <img src="images/Screenshot 2025-01-06 000850.png" height=45% width=55%/>
</p><br>

**Minimize**
Minimize action is performed when index finger and the thumb is up all together
<br><p float="left" align="center">
    <img src="images/Screenshot 2025-01-06 000918.png" height=45% width=55%/>
</p><br>

**Switch to Desktop**
When three finger Middle ,Ring , Pinky Index are UP, we switch to the desktop. More preciously the distance between Pinky and Ring is between 35-15, distance between Ring - Middle is 40-15 , and distance between Middle – Index is 35 - 15 then the switch occurs. 
<br><p float="left" align="center">
    <img src="images/Screenshot 2025-01-06 001428.png" height=45% width=55%/>
</p><br>

**Scrolling Up and Down**
Scrolling up action occurs when the Pinky ,Ring , Middle fingers are up. Scrolling down occurs when the Pinky, Ring, Middle are half bent. More preciously the distance between Pinky TIP and MCP is less than 60, Ring TIP and MCP is less than 85 and distance between Middle TIP and MCP is less than 90.

<br><p float="left" align="center">
    <img src="images/Screenshot 2025-01-06 001357.png" height=45% width=55%/><br>
    Scrolling Up<br><br>
    <img src="images/Screenshot 2025-01-06 001333.png" height=45% width=55%/><br>
    Scrolling Down<br>
</p><br>

**Switching between windows**
Switching windows on 3 phases. In first phase we need to activate the switching mode . In the second phase we need to pause switching if we reached the desired window. In the third phase we need to select it.
<br><p float="left" align="center">
    <img src="images/Screenshot 2025-01-06 001145.png" height=45% width=55%/>
</p><br>
The above gesture is for activating. In this the hand will the bent vertically and thumb will be UP and once it is tapped on the Index MCP point ,it will get activate and continuously  scroll through all the running windows.
<br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-06 001226.png" height=45% width=55%/>
</p><br>
The above gesture is to pause the scroll as  we reached our desired window.
<br>
<p float="left" align="center">
    <img src="images/Screenshot 2025-01-06 001300.png" height=45% width=55%/>
</p><br>
This is the last gesture for selecting the window or rather bringing the window  front among all the windows.

---


