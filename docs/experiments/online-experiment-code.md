---
title: Understanding how an experiment works
nav_order: 3
parent: How to build and run experiments online
---

# The jsPSych framework

## The timeline

Experiments are written in Javascript using the jsPsych library of plugins. The basic model of the code is called the `timeline`, and it's just as it sounds: each component of the experiment happens sequentially in time, and when you code the experiment, you "push" the relevant components onto the timeline.  Conceptually then, a typical  experiment that we would run in the lab looks like the diagram below.

![experiment-code-design](/online-documentation/assets/images/experiment-code-design.png)

Of course things can get more complicated than that, depending on the actual experiment, but it's useful to keep this basic model in mind as you read through the code of any particular experiment that you are building.

## Plugins

Not surprisingly, each of the differently coloured component boxes in the diagram are implemented using a different jsPsych plugin.  The `Instructions` and `End of Experiment` components typically use the `jspsych-instructions` plugin. The demographic survey code that we use uses the `jspsych-survey-html-form` plugin. The experimental stimuli use any one of a number of similar plugins. The main ones which we are likely to use in the lab are the following:

 - `jspsych-html-slider-response` used for written judgements
 - `jspsych-html-keyboard-response` used for Y/N tasks
 - `jspsych-audio-slider-response` used for spoken judgements
 - `jspsych-audio-keyboard-response` used for spoken Y/N tasks
 - `jspsych-image-slider-response`  used for image judgements
 - `jspsych-image-keyboard-response` used for image Y/N judgements
 - `jspsych-image-button-response` used for image Y/N judgements
 - `jspsych-animate` used to animate images

 Of course, images can be added to written or audio response tasks as well, so in practice we are most likely to use the first four types.

# A sample experiment

In this section we'll break down some of code of the basic written acceptability judgement task.  The basic modules of any experiment are the following:

 - Demographic survey
 - Task instructions
 - Task
 - End experiment

## The experiment timeline

The basis of all the jsPSych experiments is the *timeline*, this is an array of elements where each element of the array corresponds to one of the modules of the experiment. In our acceptabilty judgement task experiment, the main timeline will therefore ultimately look like this:

    timeline = [demographic_survey, instructions, judgement_task, end_task]

We'll see how these get put together by looking at the code directly.
