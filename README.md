****************************************************************************
Realtimeliveuserbasedvideoblur [yep, that's all one word]

http://www.jasonraimondi.com/kinect
http://deecerecords.com/kinect
Processing Authors: Jon Bellona <http://deecerecords.com>, Max Rheiner <http://iad.zhdk.ch/>
Pure Data Author: Jason Raimondi <http://www.jasonraimondi.com>

Tags: processing, pure data, kinect, simpleopenni, osc, center of mass, lumaoffset

Date: Wed 04/26/2013
Time: 12:02:29
Time Zone: (EST -05:00)

Confirmed Hardware: Early 2011 15" inch MacBook Pro, 2.2 Ghz quad i7
Confirmed OS: Mint 14 (nadia) Kernel Linux 3.5.0-17-generic 

****************************************************************************



I. Description

This archive uses real time live video blur based on users distance from the kinect. Simply put, it will track up to six users, and it will figure out who is the farthest person from the kinect, and it will blur the live video input from a webcam in realtime based on that farthest persons position. Comments are available in both the PD patches and 

II. How and Why?

I was trying to emulate vision blur on a screen in real time, based on a users distance to the screen. I ended up using the Kinect because I really wanted to use a more diverse sensor rather than just a simple, single direction ultrasonic distance sensor with an arduino, allowing only one dimension to be tracked; the Kinect allows multi user tracking and even attaches an X, Y and Z coordinate for each of the users, allowing users to be tracked in 3 dimensions. I heard about Jon Bellona and Max Rheiner's Processing project through my professor Jack Stenner and he connected me to Jon, who gladly shared his project. The project was perfect because it tracked the Center of Mass for each of the users and send it over OSC, allowing me to recieve the information in Pure Data. Pure Data allowed for the real-time video blurring. 

III. Processing

I tweaked Jon Bellona's processing code a bit, allowing you to turn on and off the GUI, and disabling the tracking of all skeletal joints, while still keeping the user and center of mass tracking. The code tracks users with the kinect, allowing Center of Mass tracking as well as Skeletal Tracking. It can then send the data for each users CoM and Skeletal information over OSC.

IV. Pure Data

A quick rundown on what is happening overall in the patch [because the patch is commented explaining what each part does]: overall, this patch is recieving (via OSC) a message called /CoM for up to six users. /CoM1, /CoM2, etc.. These OSC messages are packaged with three values, X, Y and Z. It unpacks the message to three seperate numbers, instead of a list of numbers. It takes all of the current users X, Y, and Z values, takes the maximum one out of all the X's, then all the Y's, and all the Z's (the user farthest from the camera), and lumaoffsets the video (in a value of 0 (clear) to 20 (super blurry) based on the maximum value distance. 






