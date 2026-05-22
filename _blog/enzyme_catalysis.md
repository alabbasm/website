---
layout: page
title: Notes on Enzyme Catalysis
permalink: /blog/enzyme_catalysis/
description: Recollections from Warshel, Baker, and Herschlag; Michaelis-Menten kinetics.
---

This is more for my own purpose, i will be recollecting my notes and ideas from multiple papers by notable biophysicists such as Warshel, Baker, and Herschlag. First though, should be the current approach to understanding enzyme catalysis, at least at a text book level, as well as discussion about the michaelis mentin equation, various kinetics, and some stat mech with the mass action law. Stay tuned for more tho.

# From the top, why is Chemistry even important?

Chemistry or chemical reactions to be precise, are the ways by which your body functions, how drugs are made, and even the basis of many advancements in the materials sciences, powering innovations behind better and stronger fabrics and materials. Likely, whole books can and are written about the neormous power of chemistry as a science. And catalysis is the way by which chemistry is made facile and efficient. The word catalysis has its roots in the greek word _katalysis_ which means "dissolution" or "loosening of", the formal definition was first provided by Jöns Jakob Berzelius, a Swedish chemist and phycisian who described catalysis as "(a) change caused by an agent which itself remains unchanged". Enzymes are a special type of catalysts, that are long polymers made up of repeating units or monomers called amino acids. 

[Example pic here]

The current theory as to how is often handwavy and not the focus of much of biochemustry, but essentially, enzymes function by binding the transition state (the highest energetic point of a rxn), better than the ground state (the bound enzyme substrate complex). To begin our discussion of enzymes consider the following reaction scheme

$$
E + S \underset{k_{-1}}{\overset{k_1}{\rightleftharpoons}} ES \underset{k_{-2}}{\overset{k_2}{\rightleftharpoons}} E + P
$$