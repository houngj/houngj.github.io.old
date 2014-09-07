---
title: LCF Notation
layout: default
---

I've been researching the awesome things you can do with D3.js and one of them is [building cubic hamiltonian graphs from lcf notations](http://christophermanning.org/projects/building-cubic-hamiltonian-graphs-from-lcf-notation/).

<iframe src="http://christophermanning.org/gists/1703449/#/[4]8/0/0" marginwidth="500" marginheight="500" scrolling="no" width="600" height="400"></iframe>

For those unfamiliar with hamiltonian graphs, it is a graph that contains a cycle (closed loop) that visits each node exactly once. An example of LCF notations is [2]\^4 which is a representation of a tetrahedral graph. The numbers between the square brackets are interpreted modulo N, where N is the number of vertices. The number of vertices, N, is equal to the number of elements inside of the brakets multiplied by the number outside of the brakets.

To explain how a hamiltonian graph is created through its LCF notation, lets say there exists a LCF that is [A1, A2, A3 .., An]b. Now lets say that array A = [A1, A2, A3 .., An] and that integer B = b.

The program starts with a circle graph with vertices Vertex(0) to Vertex(N-1).

> Steps:
>
> 1) Starting from Vertex(0), connect to Vertex(0) to Vertex(0 + A[0]).
>
> 2) Repeat Step1 for Vertex(1) to Vertex(N-1).
>
> 3) Repeat Step1 and Step2 B-1 times.