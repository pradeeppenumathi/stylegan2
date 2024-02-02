SUMMARY OF PAPER
GAN
Generative methods, notably Generative Adversarial Networks (GANs) [7], continually advance 
in image resolution and quality [10, 13, 2]. StyleGAN [11] is the leading high-resolution image 
synthesis method, known for its reliability across diverse datasets. This paper aims to rectify 
characteristic artifacts in StyleGAN-generated images and improve overall image quality.
StyleGAN
StyleGAN's distinguishing feature [11] lies in its unconventional generator architecture. Rather 
than directly inputting latent code z ∈ Z into the network, a mapping network f transforms it 
into an intermediate latent code w ∈ W. This w controls the synthesis network g via adaptive 
instance normalization (AdaIN) [9, 4, 6, 3], supported by additional random noise maps for 
stochastic variation. This design choice results in a less entangled intermediate latent space W, 
the focus of the analysis from the synthesis network's perspective.
Key Issues
Characteristic artifacts observed in StyleGAN-generated images [7] stem from two primary 
causes. Blob-like artifacts result from a design flaw in the generator's architecture, addressed by 
redesigning the normalization process. Artifacts related to progressive growth during training 
[10] are tackled through an alternative design without altering network topology, revealing 
lower-than-expected effective image resolution and justifying a capacity increase.
Perceptual Path Length
Quantitative analysis of image quality remains a challenge. Metrics like Frechet inception 
distance (FID) [8] and Precision and Recall (P&R) [14, 12] mainly focus on textures rather than 
shapes [5]. Perceptual path length (PPL) [11] correlates with shape consistency and stability. 
Regularizing the synthesis network to favor smoother mappings significantly enhances image 
quality. The study also reduces the frequency of regularizations to manage computational costs 
without compromising effectiveness.
Blob-Shaped Artifacts
The prevalent blob-shaped artifacts resembling water droplets found in StyleGAN-generated 
images by attributing their presence to the AdaIN operation, which normalizes feature map 
statistics and potentially disrupts feature magnitude information. Through the proposal of a 
redesigned architecture, specifically shifting bias and noise operations and introducing a 
demodulation technique replacing instance normalization within convolutional layers, the study 
successfully removes these artifacts while maintaining control over image generation. 
Architecture Change
The progressive growing technique leads to a strong preference for specific locations in the 
generated details, causing them to appear stuck or disjointed within the image. This issue arises 
because each resolution serves as the output resolution temporarily, forcing maximal frequency 
5 | P a g e
details generation, which in turn results in excessively high frequencies in intermediate layers, 
compromising the model's shift-invariance. To address this, the paper explores alternative 
network architectures, examining skip connections, residual networks, and hierarchical 
methods. Through extensive comparisons and evaluations using FID and PPL metrics, they 
identify that skip connections in the generator significantly improve PPL scores across 
configurations, while a residual discriminator network exhibits clear benefits for FID. Ultimately, 
adopting a skip generator and a residual discriminator without progressive growing 
(corresponding to configuration E) notably enhances FID and PPL scores, demonstrating a more 
effective network design for image generation
