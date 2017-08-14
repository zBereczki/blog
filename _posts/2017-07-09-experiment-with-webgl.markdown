---
layout: post
title:  "Experiment with WebGL"
permalink: /experiment-with-webgl/
date:   2017-07-09
categories:
---

In the future I would like to visualise my [model about the construction](/blog/booklet/arnyekolt_egyben_lo.jpg) with WebGL. Fortunately there is an [excellent WebGL exporter](http://www.food4rhino.com/app/iris-export-rhino-models-web) for Rhino. The next step is to embed the exported stuff into the Jekyll website. Here is my first experiment.

I used the solution from the source of this site: [https://mcneel.github.io/Iris/](https://mcneel.github.io/Iris/).

First, export the model as Iris Web Archive. The result will be a folder with some files and folders. I put the folder in a folder named `models` in the root of my Jekyll site, and used the following code, where `3r_1.iris` is the name of my Iris Web Archive folder:

`<iframe allowfullscreen id="3r_1" width="100%" height="500px" src="/blog/models/3r_1.iris/index.html" frameBorder="0" ></iframe>`

The result is here:

<iframe allowfullscreen id="3r_1" width="100%" height="500px" src="/blog/models/3r_1.iris/index.html" frameBorder="0" ></iframe>

Navigation:

- LMB - Pan around the scene
- RMB - Orbits the scene camera
- MM Wheel - Zooms
- Zooming Extents - ‘z’
- Zooming Selected - ‘s’