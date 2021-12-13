# Embody Interview Project


## How to Run 
1) Install required packages in requirements.txt
2) Download and put this <a href = https://gist.github.com/Learko/8f51e58ac0813cb695f3733926c77f52> XML file</a> in an accessible directory </br>
(This file is required for face detection)
4) Download and put this <a href = https://github.com/GuoQuanhao/68_points/blob/master/shape_predictor_68_face_landmarks.dat> dat file</a> in an accessible directory. </br> (This will be used to identify the different face points)
5) You will have to change paths in the script for both dat and XML
6) At imgs = glob.glob... you will need to have your own image dataset with this path changed too
7) Run everything cell by cell or all at once. 

## Report

Dataset and Demo </br>
- https://drive.google.com/drive/folders/1wAH4HCrhIIj1d5qMNinY88n_gB6za9J8?usp=sharing

Please write a report briefly detailing the approach you take for every solution along with the dataset/s. 
### 1 and 2 solution
- I used a small dataset of some personal pictures and then some stock photos to create the solutions for 1 & 2. 
- I was initially only focused on working with a single image. I had to google face detection methods because I did not want to reinvent the wheel. (These resources are linked below.) 
- After finding that OpenCV had a default face detector, I used that and a small function to find a face, determine if the bounding box was large enough, and then figure out if that bounding box was one that would be the 'focus face' or the one that was closest to the middle of the screen. 
### 3 and 4 solution
- Here, I found a tutorial linked below on how to implement an already trained facial focal point detector. I implemented this, which came with the video component, and was able to create a solution for 3. 
- 4 was a bit more fun. I needed to create a vector pointing from the nose of the individual. To do this, I found the center of the head's bounding box (from the facial points), and then found the focal point that corresponded to the nose (#30). I used these two points to create a vector pointing from the nose outward. While I didn't calculate an angle like the project asked me to, this vector accomplishes the exact same thing. 

### 5 
- This part was easy because of the tutorial I found below. The only thing I had to do was modify my 1 & 2 solution so it would work on video. Unfortunately drawing bounding boxes and focal points takes a little bit of time and has decreased the speed of my algorithm. Improvements could possibly be made to increase the speed of the entire algorithm. One possible solution would be to keep from passing an entire image into a function and instead figure out how to 'pass by referece' or return the focal points and bounding boxes. 

## Further Questions
- If the head goes out of focus and comes back in, will your algorithm start tracking again?
Yes. This algorithm doesn't have any memory and just tracks heads that are in each frame. 
- How are you prioritizing tracking for objects in focus?
Firstly, my algorithm only uses possible faces that have an area of at least 10% of 80% of the ROI. 
Secondly, my algorithm doesn't just prioritize a single object for the facial point part. </br>No, instead it will track facial points and poses of every head in the video. 
- Are you able to track with foreign objects like headphones, spectacles, etc?
There is a drop in performance when eyeglasses are worn. I wear eyeglasses and have noticed my program runs better when I do not have them on. I also saw no decrease in performance when I wore my airpods. Finally, there was one picture that I used to test where the algorithm had a hard time identifying a person that was wearing a hat. Since I was using off-the-shelf opencv facial detection tools, I did not prioritize improving identification with foriegn objects. 
- If there is occlusion (example: if someone is drinking from a bottle) will the tracking stop?
If a head is occluded, the object tracking performance will drop and sometimes break completely. While this could be improved if I used a NN solution, that option would slow down my algorithm. I decided to sacrifice performance for speed. (Note: The program will sometimes break if an object goes from being present to occluded. I haven't been able to successfully replicate this bug, but this is one bug I will need to fix.)
- Anything else that you think will be important for a real-world application but might not
have been mentioned above. Explain why it is important.
1) The performance of this algorithm is poor when a head goes too far to the side. Anything past a 50-60 degree angle will probably either not have facial points and/or a bounding box. If the task was instead to identify a head, no matter what the orientation, then I think this application could be useful. It would be useful because you could more easily tell what a person is paying attention to, even if they aren't looking at the screen/camera. I would implement this with something that could identify ear, chin, eye, and crown locations because this should be enough information for a person to create a 3d rotating rectangle that can represent one's head. 
2) If the goal is to use the pose to figure out what people are paying attention to, then I think it would also be useful to do some eyetracking. While I haven't implemented this yet, a person could do this by first identifying the eyes, then figuring out where the center of the eye is in relation to the pupil, and then finally get a vector from this. It seems like performance for this implementation would also be hurt by spectacles. 




## References
<a href = https://towardsdatascience.com/a-guide-to-face-detection-in-python-3eab0f6b9fc1> (Face Detection) </a></br>
<a href = https://www.pyimagesearch.com/2017/04/03/facial-landmarks-dlib-opencv-python/> (Facial Points) </a></br>


