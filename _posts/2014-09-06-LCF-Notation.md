---
title: LCF Notation
layout: default
---
<script type="text/javascript" src="http://mbostock.github.com/d3/d3.js">  </script>
I've been researching the awesome things you can do with D3.js and one of them is [building cubic hamiltonian graphs from lcf notations](http://christophermanning.org/projects/building-cubic-hamiltonian-graphs-from-lcf-notation/).

For those unfamiliar with hamiltonian graphs, it is a graph that contains a cycle (closed loop) that visits each node exactly once. An example of LCF notations is [2]\^4 which is a representation of a tetrahedral graph. The numbers between the square brackets are interpreted modulo N, where N is the number of vertices. The number of vertices, N, is equal to the number of elements inside of the brakets multiplied by the number outside of the brakets.

To explain how a hamiltonian graph is created through its LCF notation, lets say there exists a LCF that is [A1, A2, A3 .., An]b. Now lets say that array A = [A1, A2, A3 .., An] and that integer B = b.

The program starts with a circle graph with vertices Vertex(0) to Vertex(N-1).

<style>

.node {
  stroke: #fff;
  stroke-width: 1.5px;
}

.link {
  stroke: #999;
  stroke-opacity: .6;
}

</style>
<body>
<script src="http://d3js.org/d3.v3.min.js"></script>
<script>

var width = 960,
    height = 500;

var color = d3.scale.category20();

var force = d3.layout.force()
    .charge(-120)
    .linkDistance(30)
    .size([width, height]);

var svg = d3.select("body").append("svg")
    .attr("width", width)
    .attr("height", height);

d3.json("miserables.json", function(error, graph) {
  force
      .nodes(graph.nodes)
      .links(graph.links)
      .start();

  var link = svg.selectAll(".link")
      .data(graph.links)
    .enter().append("line")
      .attr("class", "link")
      .style("stroke-width", function(d) { return Math.sqrt(d.value); });

  var node = svg.selectAll(".node")
      .data(graph.nodes)
    .enter().append("circle")
      .attr("class", "node")
      .attr("r", 5)
      .style("fill", function(d) { return color(d.group); })
      .call(force.drag);

  node.append("title")
      .text(function(d) { return d.name; });

  force.on("tick", function() {
    link.attr("x1", function(d) { return d.source.x; })
        .attr("y1", function(d) { return d.source.y; })
        .attr("x2", function(d) { return d.target.x; })
        .attr("y2", function(d) { return d.target.y; });

    node.attr("cx", function(d) { return d.x; })
        .attr("cy", function(d) { return d.y; });
  });
});

</script>

> Steps:
> 1) Starting from Vertex(0), connect to Vertex(0) to Vertex(0 + A[0]).
> 2) Repeat Step1 for Vertex(1) to Vertex(N-1).
> 3) Repeat Step1 and Step2 B-1 times.