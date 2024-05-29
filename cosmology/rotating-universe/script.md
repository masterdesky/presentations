
My name is Balázs Pál, I am physics PhD student at the Eötvös Loránd University, and I do many things that is related to computational sciences. Currently I am working on an actually peculiar topic in cosmology. I am advised by several of my much more knowledgeable peers in the topic, like István Szapudi, whose original idea was this project, Gábor Rácz, who developed and currently maintains the simulation code I used and István Csabai, my actual PhD supervisor.

---
LAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZ

---

Before I talk about the details I would like to give some context for those, who are not familiar with the current state of cosmology and the motivation of research in general in this field.

Cosmology is the study of the universe and its history as a whole. Essentially, it aims to achieve two main goals:
1. To uncover and describe all physical phenomena that affect the universe on the macroscopic scale.
2. To develop a framework that can incorporate these phenomena in some unified manner... This is why cosmologists refer to such frameworks as the 'standard models of cosmology' or 'concordance cosmology'. So basically what physicists do in every single field of physics as well.

The main difference is that in cosmology this 'standard model' is just a collection of assumptions regarding the universe that every cosmological theory and model must adhere to. Currently the most widely accepted framework is the 'Lambda-CDM' model with its own unique set of assumptions. This is the theoretical side of cosmology.

The role of the observational side of cosmology is -- again, same thing that scientists (not just physicists) do in every other field -- to test and constrain both the individual models of physical phenomena and consequentially, these unified assumptions of the universe as well at the same time. However, what we saw in the last three decades is that more and more observational evidence is accumulating that is in conflict with the 'Lambda-CDM' model.

---
LAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZ

---

Now there is an even more growing disagreement on how to approach these conflicts.

Well, the situation is dire and crying seems a reasonable option, but not the only one. 

Some cosmologists argue that the 'Lambda-CDM' model is still the best model we have and that the conflicts can be ironed out in the confines of the 'Lambda-CDM' model. Some of these people believe that they are due to systematic errors in the observations, while others say the discrepancies can be tackled by introducing new physical phenomena that explains them. On the other hand, there is a growing group of people, who think that the conflicts are very real and the 'Lambda-CDM' model should be replaced with a new one entirely.

My co-authors, István Szapudi, Csabai and Gábor Rácz already had a proposal for a new model in 2017, which they called the 'AvERA' model. It describes the universe without the need of dark energy and possibly solves the Hubble tension. But in this project we went with the 'introducing a new physical phenomenon' option; namely the rotation of the universe.

Whatever that means...

The idea comes from the very simple and fundamental observation that everything in the universe rotates. From the smallest particles to the largest astronomical objects, everything spins. So why not the universe itself? We have no idea, but anyway, we are curious of what would happen, what would we observe if the universe would actually have some intrinsic rotation? This is the question we wanted to answer.

---
LAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZ

---

And we specifically wanted to answer this using numerical cosmological simulations, because... yeah, how else we're supposed to?

So far, no one has ever done this, only us. Not the cosmological simulations part in general, but the cosmological simulations of a rotating universe.

And there is a reason for that why no one has done this before. But without any humour or sarcasm, it is not good one, it is a genuinely bad 'reason'. And it is that our general approach or idea about cosmological simulations have not changed since... forever. Huge minds contributed greatly to both the theoretical and technical aspects of cosmological simulations, improving them to a level, where they could be used for precision measurements.

And of course there is a huge variety of cosmological simulations from the past 50 years, but the basic idea behind these simulations were always the same.

How do we simulate the universe? It is not different from how we simulate any other physical system.
1. We start with some initial conditions, which represents some early state of the universe with matter almost uniformly distributed,
2. Then we evolve the system over some time that represents the age of the universe,
3. And we measure the properties of the system at some later time, usually at the present time.

---
LAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZ

---

And here comes The 'basic idea' I was mentioning. For decades, cosmological simulations were always cubical and in the majority of the cases, periodic. When someone wanted to simulate the universe, they took a finite, cubical region of the universe, filled it with particles, repeated this box infinitely in all directions (periodic boundary conditions), and then solved the relevant differential equations (which is Newtonian gravity in cosmological simulations) to evolve the system in time.

This approach has both advantages and disadvantages. But the relevant one for us is that the rotation of a universe with infinite spatial extent cannot be simulated in a periodic box. István Szapudi is the one, who could tell you more about this, but a rotation would appear as a constant velocity flow inside this periodic box (which is topologically actually a 4-dimensional torus), but it won't have any acceleration, like a rotating universe should have.

Fortunately, there is another way to make cosmological simulations. We can simply set the boundary conditions to be open and isotropic and then expand the size of the box to some large value, where the boundary conditions does not affect the central part of the simulation anymore. I do not want to go into the details, but this approach is much closer to physical reality.

This is exactly what was realized for the first time by my co-authors in 2018 with some twists, when they developed the StePS simulation code, which stands for "STEreographically Projected cosmological Simulations". Very funny, because it is actually based on a fairly simple geometrical idea (stereographic projection) and it was already well-known by ancient Greek philosophers.

It works in a way that it compactifies the infinite 3D space, an infinite 3D universe into a finite 4D sphere. And due to the nature of the stereographic projection, the simulation in the real 3D space will have a gradually increasing unit volume and unit mass towards the outer boundary of the simulation. 

---
LAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZLAPOZZ

---

