---
layout: post
title: "Build Time Monitoring With Cruise"
date: 2010-01-03 20:07
comments: true
categories: [Continuous Integration, DevOps] 
---

We’ve been using [Cruise](http://www.thoughtworks-studios.com/cruise-release-management) to handle continuous integration duties on my current project for several months now. One thing that Cruise doesn’t support out of the box is any way to easily monitor the trend in build duration over time. While we as developers get a pretty good feel for the build getting slower and slower, we don’t have any real statistics that we can use as evidence to back this up.

I feel it’s very important to have a quick build, and so having visibility over build times is essential. If we’re going to make any attempt to speed up a slow build, how can we measure any improvement we make without having easy access to these statistics?

One of Cruise’s strongest features is its RESTful API which gives us the ability to integrate with it. Cruise allows access to information about past builds, including the duration which the build took to run, through its [Properties API](http://www.thoughtworks-studios.com/cruise-continuous-integration/1.2/help/Properties_API.html). This API provides access to build data in CSV format and the fact that it’s all accessible through a simple HTTP client means that it’s really easy to consume and use as you wish.

I’ve been a big fan of [jQuery](http://jquery.com) for some time, and I recently stumbled across [Flot](http://code.google.com/p/flot), which allows you to plot various different kinds of chart directly in Javascript. I’ve combined the two, with some help from the excellent [Datejs](http://www.datejs.com) library to consume the data from the Cruise API and plot the results.

{% img https://s3.amazonaws.com/anotherdeveloperblog/build-time-monitoring-with-cruise/build-times.jpeg %}

The build for our main application is divided into six stages within a single [pipeline](http://www.thoughtworks-studios.com/cruise-release-management/features-benefit). I’ve chosen to plot each stage as a separate series on the same chart, the y-axis shows the build time in minutes and seconds, and the x-axis the date on which the build took place. I’m not going to focus on we can learn form this chart in this post, but instead on how I created the chart itself. Here’s the Javascript I ended up with.

{% gist 709705 %}

I use a simple data structure to configure the URL to the Cruise properties API which will serve up the CSV (I’ve masked it in the code example), and the label which will be used to identify the series in the chart legend. I’ve only shown a single series in the code, but any number could be added to the array. Then its a case of iterating over each of the builds, using jQuery to make an Ajax call to get the CSV and parsing the result.

You’ll see I use Datejs to parse the timestamp indicating when the build took place. Cruise returns the timestamp in the format “2009-11-16 12:04:19 +1100”, which Datejs handles with ease.

You’ll also notice I only plot successful builds. I included all builds originally, but the charts became too noisy, and it made seeing the overall trend of build times difficult when failed builds were also shown.

Finally, I make use of the ajaxStop jQuery event, which is triggered when all Ajax requests are complete, at which point I plot all of the results using Flot. I’ve used a custom formatter for the y-axis, which uses Timejs (part of Datejs), to convert the build time which Cruise supplies as a number of seconds, to a more readable minutes and seconds format. I was surprised how much of a performance hit I got when rendering the chart with the custom formatter, but haven’t looked through the Timejs code to work out exactly why this is.

Within the body of my HTML page, I have a div which the result is rendered into. You’ll see it’s easy to tweak the size of the chart and other aspects to fit your requirements.

{% gist 709744 %}

I see this kind of chart working well as an [Information Radiator](http://alistair.cockburn.us/Information+radiator), giving visibilty over the trend in build time to the whole team. It would be easy to integrate this as part of your continuous integration process, and have the chart automatically redraw periodically to keep up to date with new builds. Utimately, this kind of information can be used to highlight increasing inefficiencies development teams, and their customers feel as builds get slower and to measure improvements as we work towards making the build faster.
