---
title: Online experiment basics
parent: How to build and run experiments online
nav_order: 1
---

This document outlines the basic concepts of how an online experiment works, and the different pieces you need to create in order to run one.

# Javascript, HTML and CSS

Javascript is a language that your browser interprets in order to run the experiment.  Experiments are written using a Javascript library called jsPsych. This provides large number of plugins that can be used to build the experiment.

Web pages are displayed using a combination of HTML (Hypertext Markup Language) and Javascript. The formatting of elements in displayed using HTML is determined by a separate stylesheet language called CSS (Cascading Stylesheets). Although you don't need to be an expert in any of these three components, it's important to understand how they work conceptually and what parts of the experiment are determined by them.  Schematically they look like this:

![overview](/online-documentation/assets/images/overview.png)

# Local and online versions of an experiments

We use the `cognition.run` website to host our experiments. This website uses jsPsych to generate the web pages that constitute the experiment. This means that it only requires the experiment code, stimulus file and whatever other files are used in the experiment (e.g. image files, audio files or video files). However, when we a building an experiment in the beginning, it's best to work on a local copy of the experiment, in which case we also need to provide the base HTML file to test the experiment.

The following diagram shows all of the pieces that your experiment will need. If you are just running a task with only written materials, you will only have a single stimulus file. If you are running an experiment that requires images or videos or audio files, you will have both a stimulus file along with all of the images/audio/video files.

When you run on `cognition.run`, you will add only the `.js` and `.css` files plus any additional files; you won't use the `experiment.html` file.

![experiment](/online-documentation/assets/images/experiment.png)

Notice that there are two versions of the stimulus file: one is a CSV file and the other is a `.js` file. The `.js` file is the one that is used by the experiment code, but it will be generated from a CSV file which you create using Google Sheets. The actual names of these files don't matter; I've used `experiment`, `stimulus` and `image-file` as examples.

# Basic workflow

The basic steps of designing and running an experiment are the following. Steps 1-5 are the same procedure you would use to design any experiment. Steps 6-10 are usually done together. Steps 11-16 are for actually running the experiment.

 1. Design the overall experiment (what you are testing/conditions, etc.)
 2. Decide on a method (acceptabilty judgement/truth value judgement, etc.)
 3. Create experimental materials (sentences/pictures/videos, etc.)
 4. Create filler materials (sentences/pictures/videos, etc.)
 5. Make categories of materials for analysis
 6. Create a stimulus CSV file (`stimulus-file.csv`)
 7. Convert the CSV file to JSON (`stimulus-file.js`)
 8. Code the experiment (`experiment.js`)
 9. Adjust any formatting in `experiment.css`
 9. Test the experiment locally.
 10. Create a new experiment on `cognition.run`
 11. Add the appropriate consent document to the experiment.
 11. Copy `experiment.js` into `cognition.run` and upload `experiment.css` plus any additional scripts or stimulus files
 12. Test the experiment on `cognition.run`
 13. Open the experiment up for participants.
 14. Download collected data for analysis.
