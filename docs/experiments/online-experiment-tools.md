---
title: Tools for building an online experiment
parent: How to build and run experiments online
nav_order: 2
---

This guide outlines the tools needed to build an online experiment using `jsPsych`.

# An overview of the process and tools needed

## Text editor

To edit code you need to install a plain text editor. If you're used to using
Microsoft Word, this is a different experience, since the text you're writing
doesn't get any formatting attached to it, and the format of the file is simply plain
text.

If you're already used to using a particular code editing environment, you're welcome to
use that editor, but if you're not, I recommend using Visual Studio Code, a free editor that runs on
MacOS, Windows and Linux. In these instructions I will use VSCode and if you're not using
it, I assume you know enough about coding already to adapt. You can download VSCode from this link here:

- [Download VSCode editor](https://code.visualstudio.com/download).

## GitHub

GitHub is a site which allow you to do collaborative coding using the version control system Git. All of the lab experiment code will be hosted on the lab GitHub account. It is therefore important once you begin to code an actual experiment that you have a GitHub account, and understand how to use Git.

## Google Sheets JSON converter

 The easiest way to prepare experimental materials is to use Google Sheets. This allows collaborative
 editing and the spreadsheet CSV format is how the results will be reported back for analysis. The
 jsPsych library requires the stimulus file to be in JSON format, so you will need to convert the
 Google spreadsheet into a JSON file. To do this you need to install an add-on to Google sheets.

 Go to Google Sheets and choose Get Add-ons from the Add-ons menu:

 ![google](assets/images/GoogleSheets1.png){ width=50% }\

 Choose Get Add-ons from the dropdown menu.

 ![addons](assets/images/GoogleSheets2.png){ width=30% }\

 Search for Export Sheet Data and install it.

 ![export-sheet-data](assets/images/GoogleSheets3.png)

 Once you have installed it, your dropdown menu should look like this:

 ![dropdown](assets/images/GoogleSheets4.png)


## jsPsych library

 Experiments are coded in Javascript, and use the free jsPsych library. If you are building an experiment from one of the existing lab experiments, you should simply copy that experiment. If you are building a brand new experiment, you should get the latest release of the jsPsych library here:

 - [Download latest jsPSych release](https://github.com/jspsych/jsPsych/releases)

## Cognition.run account

 Finally small experiments are run on the experiment hosting site `cognition.run`. We typically make a new account for each experiment since the free accounts are limited in the number of experiments they can run.

  - [Link to cognition.run](https://cognition.run)
  
 ## JATOS server
 
 More complex experiments are run on the lab’s experiment server. The coding of the experiment is still using jsPsych, but with some differences. It’s best to learn using `cognition.run` before learning how to code an experiment for the JATOS server.
