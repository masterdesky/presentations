
My name is Balázs Pál, I am physics PhD student at the Eötvös Loránd University, and I do many things that is related to computational sciences. Currently I am working on an actually peculiar topic in cosmology. I am advised by several of my much more knowledgeable peers in the topic, like István Szapudi, whose original idea was this project, Gábor Rácz, who developed and currently maintains the simulation code I used and István Csabai, my actual PhD supervisor.

---
'Current state of cosmology' slide - first segment

---

Before I talk about the details I would like to give some context for those, who are not familiar with the current state of cosmology and the motivation of research in general in this field.

Cosmology is the study of the universe and its history as a whole. Essentially, it aims to achieve two main goals:
1. To uncover and describe all physical phenomena that affect the universe on the macroscopic scale.
2. To develop a framework that can incorporate these phenomena in some unified manner... This is why cosmologists refer to such frameworks as the 'standard models of cosmology' or 'concordance cosmology'. So basically what physicists do in every single field of physics as well.

The main difference is that in cosmology, this 'standard model' is just a collection of assumptions regarding the universe that every cosmological theory and model must adhere to. Currently the most widely accepted framework is the 'Lambda-CDM' model with its own unique set of assumptions. This is the theoretical side of cosmology.

The role of the observational side of cosmology is -- again, same thing that scientists (not just physicists) do in every other field -- to test and constrain both the individual models of physical phenomena and consequentially, these unified assumptions of the universe as well at the same time. However, what we saw in the last three decades is that more and more observational evidence is accumulating that is in conflict with the 'Lambda-CDM' model.

---
'Current state of cosmology' slide - last line

---

Now there is an even more growing disagreement on how to approach these conflicts.

Some cosmologists argue that the 'Lambda-CDM' model is still the best model we have and that the conflicts can be ironed out in the confines of the 'Lambda-CDM' model. Some of these people believe that they are due to systematic errors in the observations, while others say the discrepancies can be tackled by introducing new physical phenomena that explains them. On the other hand, there is a growing group of people, who think that the conflicts are very real and the 'Lambda-CDM' model should be replaced with a entirely new one. But we all know, you can't just push new ideas through the scientific community.

My co-authors, István Szapudi, Csabai and Gábor Rácz already had a proposal for a new model in 2017, which they called the 'AvERA' model. It describes the universe without the need of dark energy and possibly solves the Hubble tension. But in this project we went with the 'introducing a new physical phenomenon' option; namely a sheer-free, rigid-body rotation of the universe.

Whatever that means...

The idea comes from the very simple and fundamental observation that everything in the universe rotates. From the smallest particles to the largest astronomical objects, everything spins. So why not the universe itself? We have no idea, but anyway, we are curious of what would happen, what would we observe if the universe would actually have some intrinsic rotation?

We expect that rotation would introduce an anisotropic expansion of the universe, where the expansion rate would depend on the direction we are looking at. Specifically it would depend on the axis of rotation. This is the theoretical prediction.

This is what we wanted to test this in this project. Is this effect even observable? Relevant? That's the question.

---
'Cosmological simulations' slide

---

And we specifically wanted to answer this question using numerical cosmological simulations, because... yeah, how else we're supposed to?

So far, no one has ever done this, only us. Not the cosmological simulations part in general, but the cosmological simulations of a rotating universe.

And there is a reason for that why no one has done this before. But without any humour or sarcasm, it is not good one, it is a genuinely bad 'reason'. And it is that our general approach or idea about cosmological simulations have not changed since... forever. Huge minds contributed greatly to both the theoretical and technical aspects of cosmological simulations, improving them to a level, where they could be used for precision measurements.

And of course there is a huge variety of cosmological simulations from the past 50 years, but the basic idea behind these simulations were always the same.

How do we simulate the universe? It is not different from how we simulate any other physical system.
1. We start with some initial conditions, which represents some early state of the universe with matter almost uniformly distributed,
2. Then we evolve the system over some time that represents the age of the universe,
3. And we measure the properties of the system at some later time, usually at the present time.

---
'StePS vs. the world - Boundary conditions' slide

---

And here comes The 'basic idea' I was mentioning. For decades, cosmological simulations were always cubical and in the majority of the cases, periodic. When someone wanted to simulate the universe, they took a finite, cubical region of the universe, filled it with particles, repeated this box infinitely in all directions (periodic boundary conditions), and then solved the relevant differential equations (which is Newtonian gravity in cosmological simulations) to evolve the system in time.

This approach has both advantages and disadvantages. But the relevant one for us is that the rotation of a universe with infinite spatial extent cannot be simulated in a periodic box. István Szapudi is the one, who could tell you more about this, but a rotation would appear as a constant velocity flow inside this periodic box (which is topologically actually a 4-dimensional torus), but it won't have any acceleration, like a rotating universe should have. Great, we can't use the method that everyone else used in the past 50 years.

Fortunately, there is another way to make cosmological simulations. We can simply set the boundary conditions to be open and isotropic and then expand the size of the box to some large value, where the boundary conditions does not affect the central part of the simulation anymore. And due to the geometrical attributes of the universe, we drop the cubical/toroidal topology and introduce a spherical one. I do not want to go into the details, but this approach is much closer to physical reality, than what all other simulation codes use: this periodic force calculation inside a cube with some arbitrary cut-off, which are all just for the sake of numerical convenience.

This is exactly what was realized for the first time by my co-authors in 2018 with some twists, when they developed the StePS simulation code, which stands for "STEreographically Projected cosmological Simulations". Very funny, because it is actually based on a fairly simple geometrical idea (called 'stereographic projection') and it was already well-known by ancient Greek philosophers. It is how we map the surface of a sphere to the plane. But it can be done in higher dimensions as well, this is what StePS realizes.

It compactifies the infinite 3D space, an infinite, spherical, 3D universe into a finite 4D sphere. And due to the nature of the stereographic projection, the simulation in the real 3D space will have a gradually increasing unit volume and unit mass towards the outer boundary of the simulation. 

Now one problem that comes up -- just to tell you a word about why this absolutely... unhinged idea is presented on this conference -- is that we cannot use the classical numerical methods to run this simulation. Almost every numerical trick was invented for cubical simulations in this domain. For this reason, StePS implements the most naive, direct force calculation with N^2 complexity. This is an extremely slow method, but fortunately it is a highly parallelizable problem and for this reason, StePS primarily runs on GPUs or GPU clusters. E.g. on the Wigner Scientific Computation Lab's infrastructure, like the one I used for this project. The code itself is an OpenMP-CUDA hybrid, but in this topic, Gábor Rácz, who developed it is the one, who could tell you more. I am just an active tester of the code.

---
'StePS rotating simulation' slide

---

Now that we have a code that is capable of optimally simulating a spherical, infinite universe, it becomes trivial how to determine an arbitrary rotation axis -- that e.g. runs through the center of this sphere -- and rotate the universe around it, just like we would rotate a ball.

Unfortunately, there are not just technological -- that I talked about --, but also physical problems this rotating universe introduces. Rotation appear as a form of curvature in the orthogonal direction to the rotation axis. It obviously changes the kinetic energy of particles and thus the Hamiltonian. And we need to compensate against this, because to our best knowledge, there's no curvature factor in the universe. So we scale the velocity components, orthogonal to the rotation axis in a way that have the same total energy in the system as in the non-rotating case. Minor inconvenience.

Now we can finally simulate a rotating universe and we want to run two types of simulations:
1. One with a forceless initial condition, where the universe expands, but the particles are not moving relative to each other during the simulation. We just simply place down the particles in a way that the sum of forces on them is zero. 
2. And one with a regular cosmological initial condition, where large scale structure formation is happening.

What I'm showing you in this presentation is the first type of simulations. Visually neither of them will be different, than any other forceless cosmological simulation (except that StePS is spherical), so you won't see any effect of the rotation just by looking at these images. Since the simulation is in non-comoving coordinates, what you can actually see is the expansion of the universe: We started from this little blob of particles; I zoomed into it in the middle panel. And in the right panel you can see how much the universe expanded from this initial small blob, the zoom level on the left and right panels are the same.

---
MAY OR MAY NOT TALK ABOUT THIS

---

On this bottom figure you can see something else, this is the displacement field of the simulation and we're looking at the particles from the three cardinal directions. The displacement field is what its name implies is. We connect the initial and final positions of the particles with a vector. The length of the vector is the displacement of the particle. We usually visualize this in comoving coordinates, because we don't care about the radial Hubble flow, only the movement of particles relative to each other.

If we would connect the initial and the final position of particles in the forceless case, we would see nothing, the image would be filled with zero-length vectors by definition. But slightly scaling up the final position to somehow visualize this absence of movement, we should see a figure like this.

This is what we wanted to get. Instead, it looks like this.

Now, in regular cosmological simulations, these figures always look like the fur of some animal or scratch marks on a surface. It simply means that the large scale structure formation is happening in the simulation. But in this specific case I want to present for you, it is not supposed to happen, only is simulations with the regular initial conditions.

This effect, however is extremely small. I tested it with a halo finding algorithm and although the particles moved a bit around it is still very close to a forceless simulation and no structures are formed.

---
'Measuring scale factor in orthogonal directions' slide 1.

---

What I mentioned in the beginning is that we wanted to measure, whether there is an observable difference in the expansion rate of the universe defined by the axis of rotation. We can do this by measuring the scale factor of the universe parallel and orthogonal to the rotation axis.

It is not a trivial task. The scale factor of the expansion is usually calculated with isotropy in mind, so for all particles at the same time, without any directionality. We had to invent some plausible method to measure it in two different directions. What we came up with is the following:
1. We measure the scale factor parallel to the rotation axis in two 'spherical sectors', centered on the rotation axis, but in opposite directions. These are basically conical regions of the sphere. The rotation axis was the `Z`-axis in our case, so you can see the central cross section of the two cones going up and down from the center of the sphere in the X-Z and Y-Z planes.
2. Then, we measure the scale factor orthogonal to the rotation axis in an 'equatorial belt'. This shape has no official name in geometry, but it is created by taking a 'spherical sector', like in the first case, but orthogonal to the rotation axis, then rotating it around the rotation axis. This is the belt you see on the bottom figure.

And we select them in a way that their volume is the same, and we calculate the scale factor for particles inside these regions. And we calculate it for various opening angles of the cones and the belt.

---
'Measuring scale factor in orthogonal directions' slide 2.

---

And on this slide you can see the results of these simulations and the measurement in case of the Lambda-CDM cosmology. We compared a regular, static simulation to simulations with various degrees of rotation. On this results slide specifically I show you the comparison between the non-rotating simulation and the rotating simulation with the highest possible angular velocity.

It is obvious that the non-rotating simulation has the same scale factor in all directions, as it should be (besides some numerical errors). However, the rotating simulation shows signs of strong anisotropy. 'Strong' in this case means it is an almost 2% effect, which is huge in today's precision cosmology, but it is not unusual to find these 1-2% effects in funny models like this one.

Now, what are the implications of this, can this effect be observed somehow in real measurements? This is not easy to answer, because cosmology is terrible. There are a growing number of recent articles that claim that a directional dependence of the Hubble constant can be observed in real data. But others say based on similar datasets that no, no anisotropy is present. Yeah, now you decide it.

I do not want to answer this right now, since this project in its current state is just to explore an interesting idea that many people talked about in the past, but no one ever tested numerically.

---

Thank you for your attention!