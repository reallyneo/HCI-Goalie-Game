# CS484_HCI_Goalie_Game

# - How to Run Game -
We have some dependicies that are necessary for our installation. In this zip file, we have 
run.sh, pipefile, pipfile.lock, web, and runserver.py files that will help you run this game. 
In order to start, in a python compatible terminal, run these 4 lines consecutively: 
(1) python3 -m venv flaskenv, 
(2) . flaskenv/bin/activate, or ./flaskenv/Scripts/activate for Windows
(3) pip install flask, 
(4) python3 runserver.py 11223. 

Notes:
- For some machines, it's "python" instead of "python3" for the commands above
- The project currently requires Python version 3.10.

If you're running on the display, the url to use is http://cpsc484-04.yale.internal:11223/
If you're running locally, the url is http://localhost:11223

This will begin the interactive installation. 
As you will see on the intropage screen, hover hand over the appropiate space until it fades 
away and the game screen appears. You will get 5 seconds before the game begins. Please do not 
leave screen as it will activate a pause screen that will call for you to return to the screen 
and restart the game.


# - Description of Project -
This interactive installation is a soccer goalie simulator, in which you are challenged to 
block balls from entering your goal. The two tasks our group focused on was (1) getting the 
user to physically move their body to complete an objective, and (2) pushing the user to 
complete said objective in a given time limit. The objective of blocking soccer balls is 
achieved by the user moving their hands, chest, and face to the position of an incoming soccer 
ball, achieving the first task of physical movement. We added a time limit of 1 minutes for this 
game, as the installation tracks both blocked balls (under "Score") and missed balls 
(under "Conceded"). If the user moves closer, then the goalie gets lower slightly; if the user moves
farther, then the goalie gets higher slightly. This compensates user height difference in a way.


# - Constraints -
We have some constraints for this installation. We highly suggest having the most updated 
intergrative development environment that is suitable to run python commands in the terminal. 
For certain machines, ensuring you are typing "python3" rather than just "python", is critical 
for the code to work. 

Some other constraints include:

(1) The height of the display - the display to camera height is set to be too high that when 
the user’s eyes are leveled with the screen, only half of the body can be seen. If the user 
wants to see the full body, he has to move far back, which is too far for valid sensor reading 
and visual indication. To compensate that, we made our game half-body movement only and limited 
the user interaction space to a smaller bounding box instead of the whole screen. We also made our 
interaction Z-axis independent relatively so the user doesn’t have to consider depth differences 
and can pick the best visible range for them.

(2) The latency of the sensor reading: there is about an one second delay between reading in 
the data and transmitting it through the server. So everything the user does will be behind by 1 
second. Since our game is reaction based, we had to lower the difficulty and make the ball linger 
in the area longer to account for such latency.

(3) Spatial constraints: the display is at a corner, so the user gets more space the more back 
he moves, but then the sensor data gets less accurate. There are also printer and table around the 
mid range, which added challenge to the available space of user’s movement. To account for that, we 
added a ratio to user’s x axis movement so the reading is amplified, in that when the user moves to 
the edge of the sensor, the character moves to the edge of the game space. Regarding the y axis, we 
scaled down the movement ratio so the user can stay relatively stable Y-axis wise as vertical movements 
won’t matter much due to height difference too. We think the emphasis on horizontal movement provided 
safety and flexibility in such a limited space.

(4) Technical constraints: the sensor sometimes stops reading in user input for a frame or two randomly,
and to avoid the frame data being interpreted as "user has left the scene," we added a variable numFramesTillPause
to track for the number of frames that the player isn't present in. If that accumulates above the threshold, then
the game pauses/ends. It's a measure of fault tolerance because ideally the threshold won't be triggered 
if the user still stays in place. Actually I just realized this method doesn't work because kinect cannot track
user id so it will just assign the user another id which probably doesn't match the previous id and the game
still exits anyway... nevermind... It was an attempt nonetheless. Kinect ID reassignment blocks out lots of features...





