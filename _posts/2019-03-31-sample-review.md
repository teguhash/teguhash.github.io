---
layout: post
title: A Sample Review
description: Review of something
tags:
  - sample
  - test tag
---
<dl>
  <dt>Rating:</dt>
  <dd>4.5/5</dd>
</dl>

$$ P(A | B) = \frac{P(B | A) P (A)}{P(B)} $$

I saw a $$ \pi $$ at the $$ \frac{a}{b} $$ Lorem ipsum dolor sit amet, in sed tamquam virtute disputationi. Te prima repudiare consequat nam, corpora molestie sententiae est cu. In pro dico porro meliore, nonumes facilisi sed cu. Cu eos tale summo persecuti, facete mollis in has. Albucius consequat conceptam nam te, pri augue nulla aeque ea. Vix sonet possit signiferumque at, case deleniti pro ad.

> Saperet appellantur pri id, purto ullamcorper ei eum, illud putant vituperatoribus ut vix. Eum debet discere intellegat et. Ne tollit virtute euripidis vim, unum deseruisse no sea. Ius dicit corpora interpretaris ea, nominavi legendos tincidunt in sea, usu unum sale aliquando an. Eam in nostrud adolescens philosophia.

<details><summary markdown="span">Click Me</summary>
**Quidam doctus salutatus ut eam, rebum utroque postulant ad sea, nulla munere persequeris no est. His indoctum reprehendunt id, cu consul definitionem cum. Ea meis nulla explicari usu, an vim ipsum tibique. Inani novum quaeque pro cu. Ad vis illum pertinacia, mei movet tractatos at, et solum appareat recteque usu. Feugiat patrioque nam cu, erat rationibus ut eam, erat natum option ius ut.**
</details>

Ut qui salutatus forensibus disputationi. Ad dolorum moderatius mel, graeco appetere ex pri. Saepe appetere usu at, posse laoreet offendit ea qui, mutat omnium pri no. Insolens platonem vel no, vim expetendis mediocritatem te. Voluptua mandamus senserit per in.

Te est commodo inermis consetetur. Sea te viderer vituperata, te qui falli quando verear, in nec hinc dicam. Vel decore audire disputationi te, et porro clita verterem mei, feugiat accusam vivendum sed ei. Quis putent et ius.

<style>

div.example {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}

.box {
  font: 10px sans-serif;
}

.box line,
.box rect,
.box circle {
  fill: #fff;
  stroke: #000;
  stroke-width: 1.5px;
}

.box .center {
  stroke-dasharray: 3,3;
}

.box .outlier {
  fill: none;
  stroke: #ccc;
}

</style>
<script src="https://d3js.org/d3.v3.min.js"></script>
<script src="http://bl.ocks.org/mbostock/raw/4061502/0a200ddf998aa75dfdb1ff32e16b680a15e5cb01/box.js"></script>
<script>

var margin = {top: 10, right: 50, bottom: 20, left: 50},
    width = 120 - margin.left - margin.right,
    height = 500 - margin.top - margin.bottom;

var min = Infinity,
    max = -Infinity;

var chart = d3.box()
    .whiskers(iqr(1.5))
    .width(width)
    .height(height);

d3.csv("/assets/csv/morley.csv", function(error, csv) {
  var data = [];

  csv.forEach(function(x) {
    var e = Math.floor(x.Expt - 1),
        r = Math.floor(x.Run - 1),
        s = Math.floor(x.Speed),
        d = data[e];
    if (!d) d = data[e] = [s];
    else d.push(s);
    if (s > max) max = s;
    if (s < min) min = s;
  });

  chart.domain([min, max]);

  var svg = d3.select("div#example").selectAll("svg")
      .data(data)
    .enter().append("svg")
      .attr("class", "box")
      .attr("width", width + margin.left + margin.right)
      .attr("height", height + margin.bottom + margin.top)
    .append("g")
      .attr("transform", "translate(" + margin.left + "," + margin.top + ")")
      .call(chart);

  setInterval(function() {
    svg.datum(randomize).call(chart.duration(1000));
  }, 2000);
});

function randomize(d) {
  if (!d.randomizer) d.randomizer = randomizer(d);
  return d.map(d.randomizer);
}

function randomizer(d) {
  var k = d3.max(d) * .02;
  return function(d) {
    return Math.max(min, Math.min(max, d + k * (Math.random() - .5)));
  };
}

// Returns a function to compute the interquartile range.
function iqr(k) {
  return function(d, i) {
    var q1 = d.quartiles[0],
        q3 = d.quartiles[2],
        iqr = (q3 - q1) * k,
        i = -1,
        j = d.length;
    while (d[++i] < q1 - iqr);
    while (d[--j] > q3 + iqr);
    return [i, j];
  };
}

</script>

<div id="example"></div>
