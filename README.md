# Embody Interview Project


## How to Run 
1) Install required packages in requirements.txt
2) Download and put this <a href = https://gist.github.com/Learko/8f51e58ac0813cb695f3733926c77f52> XML file</a> in an accessible directory </br>
(This file is required for face detection)
4) Download and put this <a href = https://github.com/GuoQuanhao/68_points/blob/master/shape_predictor_68_face_landmarks.dat> dat file</a> in an accessible directory. </br> (This will be used to identify the different face points)
5) You will have to change paths in the script for both of these files
6) At imgs = glob.glob... you will need to have your own image dataset with this path changed too
7) Run everything cell by cell or all at once. 

## Report

Dataset and Demo </br>
- https://drive.google.com/drive/folders/1wAH4HCrhIIj1d5qMNinY88n_gB6za9J8?usp=sharing

Please write a report briefly detailing the approach you take for every solution along with the dataset/s. 
### 1 and 2 solution

### 3 and 4 solution

### 5 


## Further Questions
- If the head goes out of focus and comes back in, will your algorithm start tracking again?
Yes. This algorithm doesn't have any memory and just tracks heads that are in each frame. 
- How are you prioritizing tracking for objects in focus?
Firstly, my algorithm only uses possible faces that have an area of at least 10% of the 80% of the ROI. 
Secondly, my algorithm doesn't just prioritize a single object for the facial point part. </br>No, instead it will track facial points and poses of every head in the video. 
- Are you able to track with foreign objects like headphones, spectacles, etc?
There is a drop in performance when eyeglasses are worn. I wear eyeglasses and have noticed my program runs better when I do not have them on. I saw no decrease in performance when I wore my airpods. There is one picture that I used to test where the algorithm has a hard time identifying a person that was wearing a hat. Since I was using off-the-shelf opencv facial detection tools, I did not prioritize improving identification with foriegn objects. 
- If there is occlusion (example: if someone is drinking from a bottle) will the tracking stop?
If a head is occluded, the object tracking performance will drop and sometimes break completely. While this could be improved if I used a NN solution, that option would slow down my algorithm. I decided to sacrifice performance for speed. (Note: The program will sometimes break if an object goes from being present to occluded. I haven't been able to successfully replicate this bug. Working on this...)
- Anything else that you think will be important for a real-world application but might not
have been mentioned above. Explain why it is important.
1) The performance of this algorithm is poor when a head goes too far to the side. Anything past a 50-60 degree angle will probably either not have facial points and/or a bouding box. If the task was instead to identify a head, no matter what the orientation, then I think this application could be useful. It would be useful because you could more easily tell what a person is paying attention to, even if they aren't looking at the the screen. I would implement this with a something that could identify ear, chin, eye, and crown locations because this should be enough information for a person to create a 3d rotating rectangle that can represent one's head. 
2) if the goal is to us the pose to figure out what people are paying attention to, then I think it would also be useful to do some eyetracking. While I haven't implemented this yet, I think a person could do this by first identifying the eyes, then figuring out where the center of the eye is in relation to the pupil, and then finally get a vector from this. It seems like performance for this implementation would also be hurt by spectacles. 




## References
<a href = https://towardsdatascience.com/a-guide-to-face-detection-in-python-3eab0f6b9fc1> (Face Detection) </a></br>
<a href = https://www.pyimagesearch.com/2017/04/03/facial-landmarks-dlib-opencv-python/> (Facial Points) </a></br>


