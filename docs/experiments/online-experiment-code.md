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

 The complete code for this experiment can be found here: [Coding Workshop](https://github.com/msu-language-acquisition-lab/CodingWorkshop)

## The experiment timeline

The basis of all the jsPSych experiments is the *timeline*, this is an array of elements where each element of the array corresponds to one of the modules of the experiment. In our acceptabilty judgement task experiment, the main timeline will therefore ultimately look like this.  In our sample experiment here we will not have a demographic survey or an explicit end task, however. 

    timeline = [demographic_survey, instructions, judgement_task, end_task]

We'll see how these get put together by looking at the code directly.

The first step is to initialize `jsPsych` and create a variable called `timeline`:

```
var jsPsych = initJsPsych({
    default_iti: 250,
    on_finish: function() {
      jsPsych.data.displayData();
    }
  });
  var timeline = [];
```

Here we supply two parameters to the initialization routine: we set a default inter-trial interval `default_iti` to 250 milliseconds, and specify what to do at the end of the experiment. The function `jsPsych.data.displayData()` displays the data collected in `json` format. This would not be used for an actual experiment, but is useful as a debugging device when developing an experiment, so we include it here. 

The `timeline` variable is defined as an array `[]`.

Next we add a basic instructions page. In this case we'll use a button press to continue to the next part of the experiment. In this toy example we don't do anything with the result of the button press, and the experiment will continue with either choice, but in practice we could have the choice end the experiment by adding an `on_finish` parameter.

```
var instructions = {
    type: jsPsychHtmlButtonResponse,
    stimulus: 'Do you want to do this experiment?',
    choices: ['Yes','No'],
  };
```
We then add this object to the timeline:

```
  timeline.push(instructions);
```
Next we create the judgement trial object. This will be repeated for each of the trial stimuli.  Here we're using the `html-slider-response` plugin.

```
 var judgement_trial = {
    type: jsPsychHtmlSliderResponse,
    stimulus: jsPsych.timelineVariable('sentence'),
    data: { sentence_type: jsPsych.timelineVariable('sentence_type'),
            expected: jsPsych.timelineVariable('expected')
    },
    labels: ['1','2','3', '4','5'],
    slider_width: 200,
    slider_start: 1,
    require_movement: true,
    prompt: '<p>How good is this sentence?</p>'
  };
```
Let's unpack the parameters we pass to this plugin. Most important is the `stimulus` parameter. We use the function `jsPsych.timelineVariable` to select the column element called `sentence` in our stimuli. This name corresponds to the column name we created in our stimulus CSV file.

Additionally, we write out using the `data` object all of the other columns in our stimulus file that we will need for analysis. Typically this will include a column that identifies the conditions in the experiment and what items are fillers, but may also include any other useful information that you may need for the future. It's always better to write extra information and ignore it later, than to forget to add information and have to add it after the fact.  In practice, when you build an actual experiment you'll get a better idea of how we use this extra data. In our simple experiment the `data` object is this:

```
data: { sentence_type: jsPsych.timelineVariable('sentence_type'),
            expected: jsPsych.timelineVariable('expected')
```

Here we've coded sentence type (which is our condition) and also what we expect the grammaticality judgement to be.

Next we set the parameters of the slider we'll use to make the judgement:

```
labels: ['1','2','3', '4','5'],
    slider_width: 200,
    slider_start: 1,
    require_movement: true,
    prompt: '<p>How good is this sentence?</p>'
```

This says that the slider will range from 1 to 5 and participants will have to interact with the slider to move on to the next trial (`require_movement:true`). We also add a prompt reminding people what the task is. 

With the judgement trial completed, we now complete the judgement task, which will loop through each stimulus item using the `judgement_trial` variable.

```
var judgement_task = {
     timeline: [judgement_trial],
     timeline_variables: stimuli,
     randomize_order: true,
   };
```

The `judgement_task` has its own internal timeline (which acts as the loop), and that timeline contains the element to be repeated on each iteration. In our case the internal timeline contains simply our `judgement_trial` variable.  The `judgement_task` object uses `timeline_variables` to specify where the stimuli are, in this case a variable called `stimuli` (which we haven't yet created, but which will be created from our stimulus CSV file and turned into a JSON variable.  Finally we tell `jsPsych` to randomize the order of the stimuli, which means we can keep our stimulus file well organized and not have to deal with randomization ourselves.

Finally we add the `judgement_task` to the experiment timeline and tell jsPsych to run it:

```
timeline.push(judgement_task);
   jsPsych.run(timeline);
```

Now our experiment is complete. 
