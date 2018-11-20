---
layout: page_no_sidebar
title: Application of robust principal component analysis (RPCA)
---

## Applications of robust principal component analysis (RPCA)
***

<div class="video_with_caption">
    <iframe width="640" height="360" src="https://www.youtube.com/embed/f5dHmRSu8mQ"  frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

    <p> OCT volume and the extracted blood vessels. (left) The OCT volume displayed as a sequence of images with each image representing the  en-face view of the skin tissue at a particular depth. The white moving clusters are the red blood cells. These moving cells show the location of blood vessels in the live skin tissue.(right) The extracted blood vessels (red mask) superimposed on the sequence of OCT images </p>
</div>
<br>

<!-- What is RPCA -->
Robust principal component analysis (RPCA) seeks to decompose a matrix into a low-rank component and a sparse component. It was found effective in many image processing problems since many real-world objects lie in a low dimensional subspace. My work is to study RPCA and use it to solve image processing problems. I found that it can be used to extract blood vessels from optical coherence tomography (OCT) data when a lab's graduate student reported his study on the blood vessel extraction problem in the lab's meeting.

<!-- Application of RPCA to blood vessel extraction -->
OCT is a biomedical optical imaging technique that enables non-invasive, high-resolution imaging of the underlying structure of biological tissue, and our goal is to extract blood vessels from 3D OCT data. I proposed a short-time RPCA method that divides the OCT data into segments and decomposes each segment into a low-rank structure representing the relatively static tissues of human skin and a sparse matrix representing the blood vessels. The method mitigates the problem associated with the slow-varying background and is free of the detection error that RPCA may have when dealing with OCT data. Both short-time RPCA and RPCA methods can extract blood vessels from OCT data with heavy speckle noise, but the former takes only half the computation time of the latter. This work was published in IEEE International Conference on Image Processing 2016 [1] and IEEE Transactions on medical imaging [2]. Even though I am the second author of both papers, I am responsible for designing the short-time RPCA algorithm.

<br>
**Publications:**  
[1] P. Lee, **C. Chan**, S. Huang, A. Chen and H. H. Chen, "Blood vessel extraction from OCT data by short-time RPCA," 2016 IEEE International Conference on Image Processing (ICIP), Phoenix, AZ, 2016, pp. 394-398. [<u>Link</u>.](/resources/BLOOD VESSEL EXTRACTION FROM OCT DATA BY SHORT TIME RPCA.pdf)  
[2] P. Lee, **C. Chan**, S. Huang, A. Chen and H. H. Chen, "Extracting Blood Vessels From Full-Field OCT Data of Human Skin by Short-Time RPCA," in IEEE Transactions on Medical Imaging, vol. 37, no. 8, pp. 1899-1909, Aug. 2018. [<u>Link</u>.](/resources/EXTRACTING BLOOD VESSEL FROM FULL-FIELD OCT DATA BY SHORT TIME RPCA.pdf)
