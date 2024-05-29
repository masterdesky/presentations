
My name is Balázs Pál, I'm PhD student at the Eötvös Loránd University studying physics, and I do many things that's related to computational sciences. I'm doing my cooperative doctoral program at the Wigner Research Centre for Physics. In the past couple months I had the opportunity to work alongside a research group at the Johns Hopkins University, the PFS Galactic Archeology Team. This is a smaller international collaboration or team that is primarily focused on doing reserach with a new instrument of the Japanese Subaru Telescope at Hawaii, called the Prime Focus Spectrograph (or PFS for short). I'll tell you more about this later.

---
LAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZ

---

But before I talk about the actual research, let me tell you what was the motivation, the scientific rationale behind it?

There is a well-known model in physics, called the "Standard Model" (with capital S and M). For those who are not physicist in the audience, this is a physical model that intends to describe three out of the four known fundamental forces in the universe. (So it can't describe gravity, but everything else.) It also aims to classify all known elementary particles and explain how these particles and fundamental forces are related to each other. We can say that it is a model that explains a certain domain of phenomena in particle physics.

It is much less known, but cosmology, the large scale study of the universe, also has its own "standard model" that intends to describe another domain of phenomena, which in this case are related to the structure and evolution of the universe. This is currently called as the "Lambda-CDM" model, but it is less established, than the Standard Model of particle physics.

In the past couple decades, let's say 30 years, many different problems of this model arised that questioned its accuracy in several topics and even its validity in general. It's still considered to be the so-called standard model of cosmology, however its problems are indisputably widespread and needs to be addressed.

And naturally, since it's such a huge field in physics, we have quite a large amount of different ways for how we can address the various challanges that LCDM has to face. Some of these ways are more direct, while some of them are... well, less direct and they consist of of a stepwise approach to these problems.

I had the chance to work on one of the myriads of approaches. My work was also just a step of the bigger picture, it was a single cog in the entire machine.

---
LAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZ

---

So what is this particular approach? It's Galactic Archeology, using the already mentioned, Subaru PFS instrument. "Galactic Archeology" is funny name I think, but it describes really well, what it's all about. Past events and processes that shaped a galaxy left marks on the stellar attributes of stars inside the galaxy, such as the chemical composition, spatial distribution, or dynamics of stars. Using these clues imprinted on stars, we can infer how a galaxy evolved in the past couple billion years. With a better understanding of galactic evolution, we can constrain the nature of the effects that influenced it in the first place. Eg. the dark matter distribution, the exact galactic halo profile of our galaxy and its satellite galaxies most importantly, etc. Successfully constraining these peculiar phenomena won't instantly solve the entire cosmology, but we'll be a step closer to an accurate and valid cosmological standard model.

------------------

Okay, but these are many consecutive steps, thata should be taken by several research groups over a span of several years. The PFS GA team is currently involved in the first phase/step, the observation and examination of the stars and stellar populations.

------------------

The best tool we have at our disposal to accurately measure many relevant stellar attributes is spectroscopy. I can mention two simple reasons, why the PFS instrument on the Subaru Telescope is interesting enough to have a collaboration formed around it and to do spectroscopy with this specific instrument:
    A) First, the telescope itself is capable of wide field observations that means many stellar objects are in the field of view of the telescope at the same time
    B) Second, the PFS instrument is desgined to be able to simultaneously measure the optical spectra of a large number of targets in the telescope's field of view with a good accuracy.
These two instruments combined will provide us a large number of high-quality spectroscopic data in the near future.

---
LAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZ

---

Yes, you heard it correctly, only in the future, we don't have real spectral data yet. So we were working with synthetic stellar spectra in the meantime to develop the pipelines that will be used to analyze the real observations, once they're ready. Now, how accurately you can simulate stellar spectra is an another topic on it own, so I won't talk about that. The only thing I'll mention is that we have a software that can generate pretty good artificial stellar spectra at least in the same parameter range that the PFS instrument will collect data from.

Here you can see what these synthetic spectra look like. They can be generated to be noisy, if we want to, as you can see on this particular visualization. The blue and gray lines are the noisy spectra in these two panels, while the orange and white lines are the pure, noiseless spectra. In the bottom panel, there are multiple spectra overimposed on top of each other, just for visual purposes, to see how large the noise is on noisy spectra.

---
LAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZ

---

Okay, but what exactly can you do with data like this? We have countless options. So what we were interested in?

We wanted to see how deep learning methods are able to tackle the different questions about stellar spectra. Of course, everyone is doing machine learning and AI for practically everything now, without any thoughtful consideration... but it was hypothesized that these methods could actually help us here.

Long story short, if you look up the literature, you'll find that there isn't any well-tested recipe on how to approach a dataset like this. So we first compiled a list of questions we wanted to answer and tried to come up with the most appropriate deep learning method for them.

------------------

The main question we wanted to answer at the end of all of this is that can a deep neural network denoise the spectra I just shown you? Observed data will be noisy, unfortunately. It would be great if an AI could just remove that noise from our data on the flip of a switch. The reason why we would love to do that is not obvious. I mean, of course, data without noise is almost always much better. There are more, but I can mention two important, direct and practical usecases of denoising:
    A) The actual existing methods for the determination of stellar parameters are simply do not work, when the noise on observed spectra are too big. If we could efficiently and accurately denoise spectra, then we could use the already existing methods to determine the stellar parameter without any problem.
    B) There is an extremely important and annoying technical detail behind a huge portion of scientific experiments. Research groups have to pay a lot of money to use a space telescope, a computing cluster, a hadron collider and many other things like that. In case of astronomical observations, you create long-exposure images of different stellar objects, to collect as much detail and to increase the signal-to-noise ratio on your observations as much as possible.

------------------

Wouldn't it be great, if we could tell details about the observed targets, even in low signal-to-noise conditions and we could spend much less time and much less money on the actual observation? That's the general usecase. In case of this project there is another similar reason. The collaboration have a large list of objets they want to observe. However many of these objects have a really high probability of being something else they expect of what that object is. And if we could tell as soon as possible that "sorry, the currently targeted object is not a red supergiant, you should start observing something else", that would save the collaboration a lot of actual time.

------------------

The very first question we wanted to answer - just to test if AI is really a walkable path here - is that whether we can encode a stellar spectra to low dimensional embedding and then reconstruct it from that? 


---
LAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZ

---

It was obvious to us at this point that we have to use some form of autoencoder network, a deep neural network architecture with an immense amount of usescases nowadays. Its so-called Encoder side basically performs a dimensionality reduction, it encodes a high dimensional data to some low dimensional representation. The Decoder side on the right then tries to reconstruct the original data from this low dimensional so-called latent space. This is exactly what we want! This is exactly what I mentioned a minute ago, what we want to do with stellar spectra in the first phase of the project.

---
LAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZ

---

After building a model and training it on synthetized data, we concluded that it worked much better than expected. In this case what happened is that we input the stellar spectra on the Encoder side of the network and we trained it in a way that the output on the Decoder side would be as similar to the original spectra as possible.

You can see these results on this slide. The top panel shows a randomly selected spectrum and its reconstructed counterpart by a trained autoencoder. They almost completely overlap, you can't really see the differences between them here on this panel.

That's why I have the bottom panel, which shows the relative errors of the reconstruction for each sample points, for each wavelengths along the synthetic spectrum. What you can see on this figure is that the hardest part for an autoencoder to learn is the exact size of the emission lines in the spectrum. The emission peaks in the spectrum are where the errors are the largest.

---
LAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZ

---

We had a lot of smaller and larger problems along the way so we were really happy to see these results, since they were much better, than previous attempts done by others in the research group. So it gave a great motivation to continue our work and see if autoencoder networks are able to denoise a spectrum.

In this particular case the input was the noisy spectra and we tried to reconstruct the noiseless, true spectra using the same autoencoder network. And you can see the results on this next slide. The second and third panel is the same as in the previous case. The top panel shows an original, noisy spectrum.

And these results are also really good. Even though you see errors reaching 15%, both the continuum and the emission lines were correctly found.

---
LAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZ

---

So what now? How to continue this? The goal we aim to reach is to reproduce the same results using an autoencoder that constists of not dense layers, but convolutional blocks. We already have some preliminary results. Convolutional neural networks, although not autoencoders, are able to classify giant stars based on their spectra.

Others also used simple CNNs, to reconstruct stellar parameters from synthetic stellar spectra and they found that these methods perform better, than dense models. Also it's hypothesized that they are much better at learning from a dataset that contains spectra with various redshifts, since convolutional models are said to be tranlation invariant in many cases. The translation in this case is obviously along the wavelength axis due to the spectrum undegoing redshifting.

So currently the main focus of our research is to test if convolutional autoencoders could really minimize the errors compared to our previous models.

An other interesting problem that we haven't tested yet is the continuum normalization. In this case the input to the deep learning model would be just a regular, noiseless stellar spectrum and we would aim to reconstruct a spectrum that has the black body continuum substracted.

Time will tell, if we're able to tackle these challanges. That's the end of my presentation, and thank you for yor attention.