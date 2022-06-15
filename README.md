# Problem

There are people that have fear of pain due to movement. This term is known as kinesophobia. With a team of physiotherapists, we propose that if the brain is tricked into believing that the patient is excecuting a movement when he/she is actually standing still, the rehabilitation process of kinesophobia will be improved. The focus will be on kinetosophobia associated with chronic low back pain. Also, of the many rehabilitation exercises we will start with the bending excercise.

```
Note: in the future there will be better cameras and more computing power to improve the size and resolution of the images.
```
# Solution proposed

![agacharse](https://user-images.githubusercontent.com/101265675/173701110-a3ecea34-627a-4acd-ae04-34fbff81cfca.png)

It is intended to trick the brain through the use of computer vision techniques. The person will wear a headset (consisting of a phone and a headset were the phone can be placed) through which he/she will observe his/her real environment. When he tries to perform the exercise and cannot continue descending due to his kinesophobia then the headset will recreate the action of bending all the way down.

# Example

A rehabilitation session of a patient at home will be recreated. 
The patient or an assistant will be asked to record the trajectory that the cell phone would have if it were to make the movement of bending all the way down. This video is shown below.

![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/101265675/173702909-b67efb60-a53e-48f0-b33c-49d60f9ad57e.gif)

Then the patient proceeds to place the cell phone inside the headset.
Once he tries to make the bending movement, he is stopped due to fear with an inclination close to 30 degrees, as it would be in this video.

https://user-images.githubusercontent.com/101265675/173672329-31cf6146-4d4c-4284-9853-6eb76358eda7.mp4

Therefore, the system is left with 2 inputs: An image corresponding to the last frame of the person bending down and a pre-recorded video.

|Last frame at 30 dregrees|Recorded video|
|---|---|
|![063](https://user-images.githubusercontent.com/101265675/173706526-db65f00d-78bb-43a6-8234-b65682c377bb.png)|![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/101265675/173702909-b67efb60-a53e-48f0-b33c-49d60f9ad57e.gif)|

**Why not just run the pre-recorded video from the position where the person stopped?**
The person is expected to be in an environment with multiple visual stimuli. That is why if you just run the video those stimuli are lost. In order to exemplify that, an alpaca stuffed animal was used. Thus, in the pre-recorded video the alpaca is not present, while in the simulation of the person bending down it is present.


## Proof of concept

The most obvious way to face this problem is to incorporate the last frame together with the pre-recorded video for a certain part of the video. For that, the most relevant action is the upward translation of the last frame. The following simulation frames show how this translation would look like. 

Frames | Frames   | Frames    
:-------------------------:|:-------------------------:|:-------------------:
 ![ 1](https://user-images.githubusercontent.com/101265675/173705950-6209c593-38fc-421c-bc79-50a2e7db7b6a.png)|![ 2](https://user-images.githubusercontent.com/101265675/173705957-7f124615-1a10-4bcc-b78a-e2fc04a725c8.png)  | ![ 3](https://user-images.githubusercontent.com/101265675/173705962-b869cfa3-068b-4a02-9871-35eaeff655fb.png)
 ![ 4](https://user-images.githubusercontent.com/101265675/173705965-7349e0c5-6400-4583-8e15-4544c9a7d446.png)|![ 5](https://user-images.githubusercontent.com/101265675/173705974-1f88aa1a-27c5-49db-bfed-0e8a4d22ecb3.png)| ![ 6](https://user-images.githubusercontent.com/101265675/173705986-4217bfeb-c4c1-435d-b696-fee22106e05c.png)
 ![ 7](https://user-images.githubusercontent.com/101265675/173705999-aa1ad69f-50e2-4942-9a33-9e451afe4242.png)|![ 8](https://user-images.githubusercontent.com/101265675/173706006-349a3612-3cb2-4ca7-abd2-15c231f2a800.png)|![ 9](https://user-images.githubusercontent.com/101265675/173706018-1863a435-55d8-4b60-a38f-40254e4c0db8.png)

The pre-recorded video can then be manipulated to run from that particular position. As can be seen in the sequence of frames below, it is practically impossible to have a good match between the translated image and the video frames.

Frames | Frames     | Frames
:-------------------------:|:-------------------------:|:-------------------:
![1](https://user-images.githubusercontent.com/101265675/173706829-64ff797b-5e99-4c91-ab5a-ff2ee89eb4cc.png)|![3](https://user-images.githubusercontent.com/101265675/173706835-ccada216-2a39-4b22-8539-216611e9b193.png)|![4](https://user-images.githubusercontent.com/101265675/173706848-c1cd08ca-2110-46f3-b585-c9e74cf7ad9f.png)
![5](https://user-images.githubusercontent.com/101265675/173706859-de8e06a9-cdc8-4e49-9312-092bc2602608.png)|![6](https://user-images.githubusercontent.com/101265675/173706865-47322321-2157-478d-b1fe-432b7a5b52e0.png)|![7](https://user-images.githubusercontent.com/101265675/173706870-68d47497-751d-4fc0-864f-4ee3e1a04274.png)
![8](https://user-images.githubusercontent.com/101265675/173706875-7e374bea-2430-49b7-b80d-e6fbf609c554.png)|![9](https://user-images.githubusercontent.com/101265675/173706886-2e203926-5c12-4158-8b55-704fa709c222.png)|![10](https://user-images.githubusercontent.com/101265675/173706891-dac84d0e-f354-4d85-9885-08e212cbacb2.png)

### Flow-edge Guided Video Completion

In order to solve this problem, the concept of video inpainting emerges as a possibility. The [FGVC](https://arxiv.org/pdf/2009.01835.pdf) paper was used, obtaining the following results.

Frames | Frames     | Frames
:-------------------------:|:-------------------------:|:-------------------:
![073](https://user-images.githubusercontent.com/101265675/173708234-e716d552-bcbb-41fc-8e98-1f0648c30a48.png)|![074](https://user-images.githubusercontent.com/101265675/173708245-41f2b5d7-a8d1-43ad-83a4-0c6782db2e0b.png)|![075](https://user-images.githubusercontent.com/101265675/173708253-40923e2a-88cc-41a1-8a37-676e1082801b.png)
![076](https://user-images.githubusercontent.com/101265675/173708259-2add4b14-bb1c-4a73-9035-7ae40a6f0fa5.png)|![077](https://user-images.githubusercontent.com/101265675/173708267-d25de3dc-516c-4e38-9de4-bdabd8728a66.png)|![078](https://user-images.githubusercontent.com/101265675/173708277-ea245f7e-c86b-42bb-be90-8ee414f05cdf.png)
![079](https://user-images.githubusercontent.com/101265675/173708282-ef211334-4991-4ee6-b58d-2a76878e0dd0.png)|![080](https://user-images.githubusercontent.com/101265675/173708291-63c78bf3-98ab-4fc2-8aa9-fa92574fef71.png)|![081](https://user-images.githubusercontent.com/101265675/173708306-ada15ab7-a9b1-4e26-895c-fe0a4cfbd55e.png)


![FGCV](https://user-images.githubusercontent.com/101265675/173709182-47833cf0-469b-439b-9165-e6ce97807a63.gif)

### Resolution-robust Large Mask Inpainting with Fourier Convolutions

Also the image inpaint techniques were used through the [LaMa](https://arxiv.org/pdf/2109.07161.pdf) technique.

Frames | Frames     | Frames
:-------------------------:|:-------------------------:|:-------------------:
![074](https://user-images.githubusercontent.com/101265675/173708420-56f06834-da60-4412-9bef-480feb3c1b50.png)|![075](https://user-images.githubusercontent.com/101265675/173708424-a9572d1f-0860-459f-bd18-2bfe7cb92e17.png)|![076](https://user-images.githubusercontent.com/101265675/173708430-d62908b1-efbc-4164-a27b-cc14f01acc80.png)
![077](https://user-images.githubusercontent.com/101265675/173708437-3f1bf8ce-e801-4136-9578-0ad9a1381638.png)|![078](https://user-images.githubusercontent.com/101265675/173708441-0fe2d000-02ab-454d-8c7e-450603f34f7c.png)|![079](https://user-images.githubusercontent.com/101265675/173708446-ffb7b102-4ae7-4178-8a0b-605a2d8713c7.png)
![080](https://user-images.githubusercontent.com/101265675/173708457-9dbd1d7f-ee79-46cc-9635-82293431e4c4.png)|![081](https://user-images.githubusercontent.com/101265675/173708458-b8ed74ae-8903-4370-a160-00782f541be1.png)|![082](https://user-images.githubusercontent.com/101265675/173708465-3575f1fa-60ec-4b13-b94f-29270f97c618.png)


![Lama](https://user-images.githubusercontent.com/101265675/173709197-106fe38d-f7c4-4457-8c7c-8bfa038d36ec.gif)




## Real reference
This is how it would be the final result if the algorith was perfect (Ignore the second part of the video were the person stands. For the proof of concept just the first half was manipulated).

![REFERENCIA](https://user-images.githubusercontent.com/101265675/173709230-05edfe17-23ba-409f-8e91-3400edfe40ff.gif)

## Thoughts

As can be seen, the results can be quite similar to what the real reference would be like. However, there are some things to take into consideration:

- The videos do not look 100% natural. An important component is missing, which is the fact of applying rotation in the last frame, not only translation. At the same time, the rotation must consider the relative depth of each object in the frame.

- The computational power required to use image/video inpaint is quite high considering that this must be a response in seconds.

- This is a simple example, but it is projected to an environment where there are multiple visual stimuli and a slight head movement of the patient.
