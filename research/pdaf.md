---
layout: page_no_sidebar
title: Phase Detection Autofocus
---

## Phase Detection Autofocus
***

<div class="video_with_caption">
    <video class="center" width="640" height="360" controls>
       <source src="/assets/rl_trad_nov_05.mp4" type="video/mp4">
    Your browser does not support the video tag.
    </video>
    <p> Comparison of autofocus performance. (left) The autofocus process produced by reinforcement learning. (right) The autofocus process produced by a traditional method [citation]. Reinforcement learning produces a smoother autofocus process in the first scene and a faster process in the second scene. </p>
</div>
<br>

Phase detection autofocus (PDAF) is a technique that uses sensors on left and right pixels to determine the relative position between the object and the focal plane. When an image is out of focus, a shift between the assembled left and right pixels is resulted, which can be used to determine the lens movement during the autofocus process. However, the presence of noise and blur often affects the accuracy of shift estimation and hence the performance of autofocus.

To overcome this challenge, I proposed a method to enhance phase detection for such sensors. A Gaussian filter is applied to overcome the adverse effect of image noise and blur. Experiments are conducted to show that the proposed method leads to a more accurate estimate of lens movement than the traditional phase correlation. This work was published in IEEE International Conference on Image Processing (ICIP) 2017 [1].

Although the Gaussian filtering technique improves the quality of phase shift measurement, it is still insufficient to guarantee a successful autofocus process. Therefore, I proposed to characterize the relation between phase shift and lens movement by a statistical model and use the Bayes' theorem to determine lens movement given a phase shift based on the learned statistical model. This work published in Electronic Imaging (EI) 2018 [2].

Motivated by recent success of deep learning in many fields, I recently used deep learning to learn PDAF. To the best of our knowledge, it is the first work that apply deep learning to autofocus in academia. I formulated the focus process as a Markov decision process and learned a policy for determining lens movement using deep reinforcement learning. I also proposed a noise-tolerant reward function to combat the noise of the phase data. Experimental results show that the method indeed improves the autofocus speed when the initial distance of the lens to the in-focus position is very large. This work was accepted by EI 2019 [3].  

<br>
**Publications:**  
[1] C.-C. Chan, S.-K. Huang, and H. H. Chen, "Enhancement of phase detection for autofocus," in Image Processing (ICIP), 2017 IEEE International Conference on, 2017, pp. 41-45: IEEE.  
[2] C.-C. Chan and H. H. Chen, "Improving the Reliability of Phase Detection Autofocus," Electronic Imaging, vol. 2018, no. 5, pp. 1-5, 2018.  
[3] C.-C. Chan and H. H. Chen, "Autofocus by Deep Reinforcement Learning
", to appear to Electronic Imaging 2019.
