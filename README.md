<img src="https://img.shields.io/badge/-Wolfram Mathematica-DD1100?style=flat&logo=wolframmathematica&logoColor=white"/>

# Quivers and Quiver mutations with Mathematica

The Mathematica notebook can be used for drawing quivers and implementing quiver mutations. The code is the basis of many of the checks and computations done in https://inspirehep.net/literature/2048053, being inspired by one of the Wolfram Demonstration projects on Cluster Algebras. 

### What are quivers?

To understand what is a quiver, let's first talk about graphs. A <b>graph</b> (not to be confused with a plot!) is a structure that consists of a set of nodes (or vertices), and a set of relations between the nodes. These relations are marked by edges that connect the nodes. Think of this as a group of people, where we show whether two people know each other by drawing an edge between them, as in the figure below:

<p align="center">
  <img  width="400" height="300" src="https://github.com/magurh/Quivers/assets/122356566/ec847ec6-d99e-4e2c-8882-3c4be0b1ba4c">
</p>

A <b>quiver</b> is a directed graph, meaning that each edge is replaced by an arrow. This could perhaps model some telecommunications system, where an arrow between nodes (people) $i$ and $j$ says that person $i$ is calling person $j$. A natural way of representing a quiver is through an adjacency matrix $B$, whose entries $B_{i,j}$ correspond to the number of arrows from node $i$ to node $j$.


### Why are we interested in Quivers?

Having introduced quivers, the next question is why such objects would be of interest to physicists. It turns out that there is a nice interpretation of them in the framework of Quantum Field Theory (QFT). QFT combines ideas from special relativity, quantum mechanics and classical field theory, an example of which is the theory of Electromagnetism. Let me only focus on the latter here and sweep under the rug the differences between classical and quantum field theories.

In the context of electromagnetism, we often talk about electric charge and how this affects the interactions between charged particles, such as electrons. More formally, we say that electric charge is the generator of a certain symmetry of electromagnetism, called a $U(1)$ symmetry.

Symmetries are ubiquitous in physics, and a very beautiful theorem due to Noether states that for every (continuous) symmetry of the model there is a conserved charge, which, in this scenario, is the electric charge. Similar statements exist for energy and momentum conservation laws.

Alright, so electromagnetism is a theory with a $U(1)$ symmetry. The models that I am interested in are generalisations of electromagnetism (or, rather of quantum electrodynamics, which is the quantum field theory version of electromagnetism), in which there can be multiple such symmetries. As such, we represent eac symmetry by a node of a quiver, while the arrows will tell us something about the 'charges' of the matter fields. 

### Quivers and Quiver Mutations

The notebook implements a function DrawQuiverInt[] for drawing a quiver from its adjacency matrix (also referred to as the intersection matrix in the notebook). A natural operation on quivers is a 'mutation'; this turns out to have deep physical implications, with the models related by mutations being (Seiberg) 'dual' to each other. Mutations can be implemented in three steps:

1. Pick a node to mutate on, call it $M$.
2. For each length 2 path going through nodes $i-M-j$, draw an arrow from node $i$ to node $j$.
3. Reverse all the arrows connected to node $M$.

In this algorithm, 'bidirectional' arrows will simply cancel each other. The DrawQuiverInt[] allows one to mutate on any node of choice, and also increase the number of mutations. An example is shown below:

<p align="center">
  <img  width="850" height="400" src="https://github.com/magurh/Quivers/assets/122356566/bfd90a08-a144-4fa3-b25a-2e2f897bf8ca">
</p>


### Details for the experts

A quiver can be also drawn from a basis of BPS states. Given a basis of $n$ states, the adjacency matrix can be obtained using IntersectionMatrix[n, Q], where Q is a list of the magnetic-electric charges {m, n}. It is also convenient, at times, to obtain the charges after a quiver mutation, rather than the new adjacency matrix. For this, we implement the function MutationsForCharges[Q, Mut], with Mut a list of mutations of the type {node, r}. Here r is either 0 or 1, depending on whether we do a clockwise or anti-clockwise mutation.

This algorithm was the foundation of many of the examples presented in the publication https://inspirehep.net/literature/2048053.



