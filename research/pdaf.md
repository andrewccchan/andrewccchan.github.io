---
layout: page_no_sidebar
title: Phase Detection Autofocus
---

## Phase Detection Autofocus
***

<div class="video_with_caption">
    <iframe width="640" height="360" src="https://www.youtube.com/embed/sN6z8ccjg8o" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

    <p> Comparison of autofocus performance. (left) The autofocus process produced by reinforcement learning. (right) The autofocus process produced by a traditional method [citation]. Reinforcement learning produces a smoother autofocus process in the first scene and a faster process in the second scene. </p>
</div>
<br>

Phase detection autofocus (PDAF) is a technique that uses sensors on left and right pixels to determine the relative position between the object and the focal plane. When an image is out of focus, a shift between the assembled left and right pixels is resulted, which can be used to determine the lens movement during the autofocus process. However, the presence of noise and blur often affects the accuracy of shift estimation and hence the performance of autofocus.

To combat the noise of phase information, I studied the raw images and the point spread function of the camera to figure out the cause of the noise. Through this process, I realized that the quality of phase information could be greatly improved by simply applying a Gaussian filter to the correlation curve. (A correlation curve represents the correlation between the assembled left and right pixels at different amounts of shift.) This work was published in IEEE International Conference on Image Processing (ICIP) 2017 [1].

Although the Gaussian filtering technique improves the quality of phase shift measurement, it is still insufficient to guarantee a successful autofocus process. Therefore, I proposed to characterize the relationship between phase shift and lens movement by a statistical model and use the Bayes' theorem to determine lens movement given a phase shift based on the learned statistical model. This work published in Electronic Imaging (EI) 2018 [2].

Both approaches above are not able to utilize information from an early stage of an autofocus process in the latter stage. Motivated by recent successes of deep learning in many fields, I used a recurrent neural network, which can effectively utilize the history, to learn the autofocus process and trained the network by deep reinforcement learning. I also proposed a noise-tolerant reward function to combat the noise of the phase data. Experimental results show that the method indeed improves the autofocus speed when the initial distance of the lens to the in-focus position is very large. This work was accepted by EI 2019 [3]. To the best of our knowledge, this is one of the first data-driven approaches to autofocus and may serve as a foundation for future research in PDAF.

<br>
**Publications:**  
[1] **C. Chan**, S. Huang and H. H. Chen, "Enhancement of phase detection for autofocus," 2017 IEEE International Conference on Image Processing (ICIP), Beijing, 2017, pp. 41-45. [<u>Link</u>.](/resources/ENHANCEMENT OF PHASE DETECTION FOR AUTOFOCUS.pdf)  
[2] **C. Chan** and H. H. Chen, "Improving the Reliability of Phase Detection Autofocus," Electronic Imaging, vol. 2018, no. 5, pp. 1-5, 2018.  [<u>Link</u>.](/resources/IMRPOVING THE RELIABILITY OF PHASE DETECTION AUTOFOCUS.pdf)  
[3] **C. Chan** and H. H. Chen. "Autofocus by Deep Reinforcement Learning," accepted by  Electronic Imaging 2019. [<u>Link</u>.](/resources/AUTOFOCUS BY REINFORCEMENT LEARNING.pdf)
