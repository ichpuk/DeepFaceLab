### **Model types**:

- **H64 (2GB+)** - half face with 64 resolution. It is as original FakeApp or FaceSwap, but with new TensorFlow 1.8 DSSIM Loss func and separated mask decoder + better ConverterMasked. for 2GB and 3GB VRAM model works in reduced mode.

H64 Robert Downey Jr.:

![](https://github.com/iperov/DeepFaceLab/blob/master/doc/H64_Downey_0.jpg)

![](https://github.com/iperov/DeepFaceLab/blob/master/doc/H64_Downey_1.jpg)

- **H128 (3GB+)** - as H64, but in 128 resolution. Better face details. for 3GB and 4GB VRAM model works in reduced mode.

H128 Cage:

![](https://github.com/iperov/DeepFaceLab/blob/master/doc/H128_Cage_0.jpg)

H128 asian face on blurry target:

![](https://github.com/iperov/DeepFaceLab/blob/master/doc/H128_Asian_0.jpg)

![](https://github.com/iperov/DeepFaceLab/blob/master/doc/H128_Asian_1.jpg)

- **DF (5GB+)** - @dfaker model. As H128, but fullface model. Strongly recommended not to mix various light conditions in src faces.

![](https://github.com/iperov/DeepFaceLab/blob/master/doc/DF_Cage_0.jpg)

- **LIAEF128 (5GB+)** - Less agressive Improved Autoencoder Fullface 128 model. Result of combining DF, IAE, + experiments. Model tries to morph src face to dst, while keeping facial features of src face, but less agressive morphing. Model has problems with closed eyes recognizing.

LIAEF128 Cage:

![](https://github.com/iperov/DeepFaceLab/blob/master/doc/LIAEF128_Cage_0.jpg)

![](https://github.com/iperov/DeepFaceLab/blob/master/doc/LIAEF128_Cage_1.jpg)

LIAEF128 Cage video:

[![Watch the video](https://img.youtube.com/vi/mRsexePEVco/0.jpg)](https://www.youtube.com/watch?v=mRsexePEVco)

- **SAE (2GB+)** - Styled AutoEncoder - new superior model based on style loss. Morphing/stylizing done directly by neural network. Face obstructions also reconstructed without any masks. Converter mode 'overlay' should be used. Model has several options on start for fine tuning to fit your GPU.

![](https://github.com/iperov/DeepFaceLab/blob/master/doc/SAE_Cage_0.jpg)

![](https://github.com/iperov/DeepFaceLab/blob/master/doc/SAE_Cage_1.jpg)

![](https://github.com/iperov/DeepFaceLab/blob/master/doc/SAE_Navalniy_0.jpg)

SAE model Cage-Trump video: https://www.youtube.com/watch?v=2R_aqHBClUQ

SAE model Putin-Navalny video: https://www.youtube.com/watch?v=Jj7b3mqx-Mw


### **Tips and tricks**:

unfortunately deepfaking is time/eletricpower consuming topic and has a lot of nuances.

Every model is good for specific scenes and faces.

H64 - good for straight faces as a demo and for low vram.

H128 - good for straight faces, gives highest resolution and details possible in 2019. Absolute best for asian faces, because they are flat, similar and evenly lighted with clear skin.

DF - good for side faces, but results in a lower resolution and details. Covers more area of cheeks. Keeps face unmorphed. Good for similar face shapes.

LIAE - can partially fix dissimilar face shapes, but results in a less recognizable face.

SAE - no matter how similar faces, src face will be morphed onto dst face, which can make face absolutely unrecognizable. Model can collapse on some scenes. Easy to overlay final face because dst background is also predicted.

Quality of src faceset significantly affects the final face.

Narrow src face is better fakeable than wide. This is why Cage is so popular in deepfakes.

SAE tips:

- if src faceset has number of faces more than dst faceset, model can be not converged. In this case try 'Feed faces to network sorted by yaw' option.

- if src face wider than dst, model can be not converged. In this case try to decrease 'Src face scale modifier' to -5.

- architecture 'df' make predicted face looking more like src, but if model not converges try default 'liae'.

- most scenes converge fine with batch size = 8. In this case better to increase 'encoder/decoder dims per channel' to get more sharp result.
