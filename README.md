# Udacity_Robo_search :
## submission note along with rubrics 
![project result ](https://github.com/spicecoder/Udacity_Robo_search/blob/master/auto-robot1.png "autonomous mode")
This is my first project  submission in the Udacity Robotics Software Engineer Nanodegree "Program Search and Sample Return "

The projects allows us to build algorithmic skills in the three foundational principles of robotics operation  namely : Perception,Decesion and Action.


The task being operating a simulated robot ,lets call it simbo , ie a robot that has been simulated in the  Unity  softwrae platform which ,being a gaming platform, allows a realistic creation of terrains with mountains and sands where our little friend simbo  moves around. 

Before writing program code that will interact with simbo , we are allowd to operate the robot on our screen using mouse and keys. As we operate simbo , we come across some yellow rocks that are spread around the terrain at various spots [we have been told they are always near the walls!]  and simbo can pick those at our command. 
This way  one can really get fond of simbo's semi gracious move to pick the yellow stones and carefully place them at the back of the truck that simbo is riding on. 


After playing with simbo for a while, we are ready to start recording the immediate scenes that simbo's alert eyes can capture through an inbuilt 'camera' in the simulator -which simulates the robots camera. The screens are recorded at a rate ofabout  20 per second and the data are captured in a CSV file. In a real robot these scenes are fed constantly to the robots perception mechanism and by recording these data we get enough test data that we can use to build our algorithim  that will guide simbo to move around autonomously , without being driven by our mouse and keyboards.


At this point it is better to clarify , the challenge for me ,the student here,is in two spaces
  i. write algorithim to guide simbo
  ii. bind these algorithims to the simulation software built by udacity on which simbo lives.
I enjoyed the challenge in both the spaces; My guess, the first assignment works as an  upfront exposure of the environment before starting a Robotics journey . I am looking forward to making the algorithims developed for this assigment to more comprehesive solutions as we progress along the course.


Now, about the details in the assignment submission.
The percption part comprises in breaking up each of these visible snapshot screen in the pixel-areas of obstacle, navigable and collectable rocks.
For simbo they are all a collection of pixels within certain colour threshhold. The task is made simpler for us because Udacity created the mountains [obstacles] and navigable terrain with distinct colour variation ;  So we capture the picture, perform color analysis and pick up navigable pixel coordinates, using a color threshold to extract navigable regions. 

 For  identifying yellow rocks we  specify two color thresholds  above and below for yellow and then identify rocks as those pixels that are only found when falls within this threshold.


 The coodinates from simbos camera coordinates, transformed  through to polar coordinates that are transformed into world coordinates .

Transforming to world coordinates help us manipulate the robot with respect to obstacles around and keep track of the fidelity of our map against the ground truth which is derived from a callibration black and white image.

The color_thresh function in perception.py file takes care of filtering the pixels suitable for Obstacles, Samples and the ground. While Udacity provides most of the code snippets I had to complete the perception_step function in Percpetion.py  to bring the functions work in sequence to get the polar coordinates into Rover's attributes to be accessed in the decesion process.

Once we get the navigable pixels at any pont in time as simbo throttles ahead , we can keep simbo on course by more or less the median angle from the spread of navigable pixels, with some offset to be biased towards the wall and keep steering in the right direction so Simbo does not land aginst obstacle and gets stuck at one point. The decesion.py file has got the decesion logic to make the Rover go forward ,stop , change direction. Again Udacity provides the function codes that can be used in my task to set up the  the decesion step which I make use of change in position ,and the total time and start time of the Rover provided through the supporting_functions.py. 

One can get creative and make interesting moves here - I was getting problem when simbo was getting stuck against a particular mountain rock that seemed to be hanging above ground and the navigable median is pointing straight to the rock and even after getting stuck simbos camera was showing clear navigable area ahead. 

I put some code to do some randomly generated  steering angles- which works some time, if the position of robot does not change over subsequent snapshots. I have not found a solution when simbos tyre gets caught in the sand and simbo can not free it without manual intervention.


Although I still donot have the complete list of commands offered by the simulation environment that simbo understands the  much quoted list of commands like :steering, throttle, brake, speed, position, pitch, yaw and roll-   seems to have done a good enough job for the assignment -which is to just locate at least one rock and move around autonomously.
It is also bit late to ask these questions to the mentor who have been quite helpful along the way ,however,
I would like to go through the commands available for the simulated robot before thinking about the correct solution in the above two cases.

Also I feel the protrayed navigable region is too sensitive to the pitch angle and also the distance of the obstacle from the camera is not represented in a favourable way for navigation purpose. Both these factors can be addressed by determining  ground navigation as the resultant effect from two views of camera -one pointing horizontal and another pointing at an angle to the ground and determine the pixel count from their average. -this will also help in overcoming the effect of ground elevation and roughness.

However I feel , I could be in a better position to even meet the extra challenge attched to this project , namely for simbo to actualy collect rocks and return to its starting point - if only  I could have had a much clearer picture of what I am supposed to address right from start- instaed of throwing myself into idiosynchracies of python notebook,Roversim , and code snippets depenencies- kind of  lost the forest in the trees for simbo. Possibly Roversim can evolve ,for future students, to be an environment for a student to organise the artifacts needed to make simbo to be self sufficient. 

The fidelity achieved in the autonomous mode is more than 78 % with ground coverage more than 58%. 
The Roversim was run with screen resolution 1024 x 768 . 
The data recorded by me in training mode are in the folder recorded_data. The recorded output video is in output/recorded_mapping.mp4.


