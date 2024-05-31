
My name is Balázs Pál, I am physics PhD student at the Eötvös Loránd University and at the Heavy-Ion group at Wigner.

I am really glad that for this very first presentation of the day I can present you a funny little project that I am currently working on. I am advised by several of my much more knowledgeable peers in the topic, like István Szapudi, whose original idea was this project, Gábor Rácz, who developed and currently maintains the simulation code I'm using and István Csabai, my actual PhD supervisor. All of us are part of István Csabai's astro/cosmo research group.

---
'Current state of cosmology' slide - first segment

---

This topic is from the field of computational cosmology. So whether you're familiar with it or not, please let me give you some context first. Primarily about the current state of cosmology and the motivation of this project and research in general in this field.

We usually say that cosmology is the study of the universe and its history as a whole. But essentially, it aims to achieve two main goals:
1. To uncover and describe all physical phenomena that affect the universe on the macroscopic scale.
2. To develop a framework that can incorporate these phenomena in some unified manner... This is why cosmologists refer to such frameworks as the 'standard models of cosmology' or 'concordance cosmology'. So basically what physicists do in every single field of physics as well.

The main difference is that in cosmology, this 'standard model' is just a collection of assumptions about the universe, and every cosmological theory and model must adhere to them. Currently the most widely accepted such framework is the 'Lambda-CDM' model with its own unique set of assumptions. This is the theoretical side of cosmology.

The role of the observational side of cosmology is to test and constrain both the individual models of physical phenomena and consequentially, these unified assumptions of the universe as well at the same time. But, what we saw in the last couple decades is that more and more observational evidence is accumulating that is in conflict with the 'Lambda-CDM' model.

---
'Current state of cosmology' slide - last line

---

Now there is an even more growing disagreement on how to approach these conflicts.

Some cosmologists argue that they can be ironed out in the confines of the 'Lambda-CDM' model. Some of these people believe that they are due to systematic errors in the observations, while others say the discrepancies can be tackled by introducing new physical phenomena that explains them. On the other hand, there is another growing group of people, who think that the conflicts are very real and the 'Lambda-CDM' model should be replaced with a entirely new one. But we all know, you can't just push new ideas through the scientific community, so despite all problems, the LCDM model still holds strong.

And although the group of István Csabai already had a proposal for a new model in 2017, which they called the 'AvERA' model, in this project we went with the 'introducing a new physical phenomenon' option; namely a sheer-free, rigid-body rotation of the universe.

Whatever that means...

The idea comes from the simple observation that everything in the universe rotates. From the smallest particles to the largest astronomical objects, everything spins. So why not the universe itself? We have no idea, but anyway, we are curious of what would happen, what would we observe if the universe would actually have some intrinsic rotation?

We expect that a rotation would introduce an anisotropic expansion of the universe, so the expansion rate would depend on the direction we are looking at. Specifically it would depend on the axis of rotation. This is the theoretical prediction.

And we wanted to test, whether this effect is even observable? Relevant? That's the question.

---
'Cosmological simulations' slide

---

And we specifically wanted to answer this question using cosmological simulations, because... yeah, how else we're supposed to?

So far, no one has ever done this. Not the cosmological simulations part in general, but the cosmological simulation of a rotating universe.

And there is a reason for why no one has done this before. It is that our general approach or idea about cosmological simulations have not changed since... forever. Of course there is a huge variety of cosmological simulations from the past 50 years and they improved tremendously, but the basic idea behind these simulations were always the same.

How do we even do cosmological simulations?
1. We start with some initial conditions, which represents some early state of the universe with matter almost uniformly distributed,
2. Then we evolve the system over some time that represents the age of the universe,
3. And we measure the properties of the system at some later time, usually at the present time.

---
'StePS vs. the world - Boundary conditions' slide

---

And here comes The 'basic idea' I was mentioning. For decades, cosmological simulations were always cubical and in the majority of the cases, periodic. When someone wanted to simulate the universe, they took a finite, cubical region of the universe, filled it with particles, repeated this box infinitely in all directions (periodic boundary conditions), and then solved the relevant differential equations (which is Newtonian gravity in cosmological simulations) to evolve the system in time.

This approach has both advantages and disadvantages. But the relevant one for us is that the rotation of a universe with infinite spatial extent cannot be simulated in a periodic box. István Szapudi is the one, who could tell you more about this, but a rotation would appear as a constant velocity flow inside this periodic box (which is topologically actually a 4-dimensional torus -- NEXT ANIMATION --), but it won't have any acceleration, like a rotating universe should have. Great, we can't use the only method that everyone else used in the past 50 years.

Fortunately, there is another way to make cosmological simulations and it is exactly what was done for the first time by the group of István Csabai in 2018 with some twists, when they developed the StePS simulation code, which stands for "STEreographically Projected cosmological Simulations". The general idea is to drop the translational invariance of the classical periodic simulations in favor of rotational invariance.

The way StePS realizes this is very funny, because it is actually based on a fairly simple geometrical idea ('stereographic projection'), which was already well-known by ancient Greek philosophers. István Szapudi regularly mentions how much he's baffled that no one ever tried this before them. So this stereographic project is the method to map the surface of a sphere onto the entire plane. However, it can be generalized for higher dimension and this is exactly what StePS does.

It compactifies the infinite 3D space, an infinite, spherical, 3D universe into/onto a finite 4D sphere. Due to the nature of the stereographic projection, the simulation in the real 3D space will have a gradually decreasing resolution as we move away from the center of the sphere. I do not want to go into the details, but this approach, where an infinite universe with a rotational symmetry is realized, it is much closer to physical reality, than the classic method: this periodic force calculation inside a cube with some arbitrary cut-off distance for the force calculation, which are all just for the sake of numerical convenience.

---
'StePS rotating simulation' slide

---

Now that we have a code that is capable of simulating a spherical, infinite universe, it becomes trivial how to define an arbitrary rotation axis -- e.g. one that runs through the Z-axis (this is what I used in these simulations) -- and then we can simply rotate the universe around it, just like we would rotate a ball. We want to run two types of simulations:
1. One with a forceless initial condition, where the universe expands, but the particles are not moving relative to each other during the simulation. We just simply place down the particles in a way that the sum of forces is zero. 
2. And one with a regular cosmological initial condition, where large scale structure formation is happening.

What I'm showing you in this presentation is the first type of simulations. Visually neither of them will be different, than any other cosmological simulation (except that StePS is spherical), so you won't see any effect of the rotation just by looking at these images. Since the simulation is in physical/proper coordinates, what you actually can see is the expansion of the universe: We started from this little blob of particles; I zoomed into it in the middle panel. And in the right panel you can see how much the universe expanded from this initial small blob, the zoom level on the left and right panels are the same.

--- BOTTOM FIGURE; DISPLACEMENT FIELD ---

On this bottom figure you can see something else, this is the displacement field of the simulation and we're looking at the particles from the three cardinal directions. The displacement field is what its name implies it is. We connect the initial and final positions of the particles with a vector. The length of the vector is the displacement of the particle. We usually visualize this in comoving coordinates, because we don't care about the radial Hubble flow, we know it's there, we only care about the movement of particles relative to each other.

If we would plot the displacement field in a forceless simulation -- like the one we have here --, we would see nothing. The image would be filled with zero-length vectors by definition. Forceless initial conditions, comoving coordinates, no movements. Instead, it looks like this.

Here the X-Y plane beautifully shows the rotation around the Z-axis. On the other hand, the other two panels shows that our initial conditions were not the best. In regular cosmological simulations, these figures always look like the fur of some animal. It simply means that the large scale structure formation is happening in the simulation. But ideally, in this case it not supposed to happen.

Fortunately this effect is extremely small. I tested the final state of the simulation with a halo finding algorithm and although the particles moved around a bit, it is still very close to a forceless simulation and no structures or halos were formed.

---
'Measuring scale factor in orthogonal directions' slide 1.

---

What I mentioned in the beginning is that we wanted to measure, whether there is an observable difference in the expansion rate of the universe defined by the axis of rotation. We can do this by measuring the scale factor of the universe parallel and orthogonal to the rotation axis.

It is not a trivial task. The scale factor of the expansion is usually calculated with isotropy in mind, so for all particles at the same time, without any directionality. We had to invent some plausible method to measure it in two different directions. After some trial and error, what we came up with is the following:
1. We measure the scale factor parallel to the rotation axis in two 'spherical sectors', centered on the rotation axis, but in opposite directions. These are basically conical regions of the sphere. Since the rotation axis was the `Z`-axis in our case, you can see the central cross section of the two cones going up and down from the center in the X-Z and Y-Z planes.
2. Then, we measure the scale factor orthogonal to the rotation axis in an 'equatorial belt'. This shape has no official name in geometry, but it is created by taking a 'spherical sector', like in the first case, but orthogonal to the rotation axis, then rotating it around the rotation axis to create a solid of revolution. This is the belt you see on the bottom figure.

We select both of these in a way that their volume is equal, and we calculate the scale factor for particles inside these regions. And we calculate it for various opening angles of the cones and the belt.

---
'Measuring scale factor in orthogonal directions' slide 2.

---

And on this slide you can see the results of these simulations and the measurement in case of the Lambda-CDM cosmology. We compared a regular, static simulation to simulations with various degrees of rotation. On this results slide specifically I show you the comparison between the non-rotating simulation and the rotating simulation with the highest possible angular velocity. On the X-axis you can see billion years and on the Y-axis the scale factor of the universe, which is by convention equals to 1 at the present time.

It is obvious that the non-rotating simulation has the same scale factor in all directions, as it should be (besides some numerical errors). However, the rotating simulation shows signs of strong anisotropy. 'Strong' in this case means it is an almost 2% effect, which is huge in today's precision cosmology, but it is not unusual to find these 1-2% effects in funny models like this one.

Now, what are the implications of this, can this effect be observed somehow in real measurements? This is not easy to answer, because cosmology is terrible. There are a growing number of recent articles that claim that a directional dependence of the Hubble constant can be observed in real data. But others say based on similar datasets that no, no anisotropy is present. Yeah, now you decide it.

I do not and cannot want to answer this right now, since this project in its current state is just to explore an interesting idea that many people talked about in the past, but no one ever tested numerically.

---

Thank you for your attention!