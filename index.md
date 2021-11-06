---
layout: home
title: Advanced Data Science
---

The Advanced Data Science unit will set the context on the emerging domain of data science and guide students through the data science pipeline. At the end of the course students will be familiar with the purpose of data science, how it differs from the closely related fields of machine learning, statistics and artificial intelligence and what a typical data analysis pipeline looks like in practice. As well as emphasising the importance of analysis methods we will introduce a formalism for organising how data science is done in practice and what the different aspects the data scientist faces when giving data-driven answers to questions of interest.

Your assessment is [available in Moodle](https://www.vle.cam.ac.uk/). The assessment is tightly integrated with the course lecturing, it is staged so that you should be able to make a start on the first question as soon as you've finished Lab Session One. Your assessment should progress alongside the course with different questions becoming easier to answer as you complete each of the labs.

* [Discussion forum for the module on Reddit](https://www.reddit.com/r/CST_ADS/).

*If this page isn't rendering properly for you, it's likely because your ad-blocker is stopping the CSS loading (the base url is "ads").*

## Lectures

{% assign lastone = site.lectures | last %}
{% for lecture in site.lectures %}
{% include listlecture.html %}
{% endfor %}
