---
# Documentation: https://hugoblox.com/docs/managing-content/

title: "DeepHyper Collaboration"
summary: "A collaboration with the team developing DeepHyper on an 11 months contract as a research aide. Development of benchmarks and analytical tools to help improving the package followed by an application of its AutoML methods to a real-case Deep Learning problem."
authors: [admin, Prasanna Balaprakash, Romain Egele, Kyle Gerard Felker]
tags: [research, contract]
categories: [research, fixed-term contract]
date: 2022-10-04T16:41:46+01:00

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: "Image credit: [**DeepHyper**](https://deephyper.github.io/)"
  focal_point: ""
  preview_only: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: DeepHyper
#   url: https://github.com/deephyper/deephyper

url_code: "https://github.com/deephyper/deephyper"
url_pdf: "project/deephyper/Internship_Report_ANL.pdf"
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---

## Summary

This work was led during a gap year between my 2nd and 3rd years of engineering studies, and took the form of a Research Aide contract in remote from France with the team developing [DeepHyper](https://deephyper.github.io/), at the [Argonne National Laboratory](https://www.anl.gov/) (ANL), United STates, under the supervision of Prasanna Balaprakash and Romain Egele.

The main goal was to contribute to the improvement of the scalability of DeepHyper, by developing benchmarks, testing modules, algorithms, and conducing eperiments with the package.
The provided PDF is only a short report, you can find more details below. 

## Contribution to the Package

DeepHyper is a scalable package for Automated Machine Learning, especially developing Black-Box Optimization (BBO) and Neural Architecture Search (NAS) methods that can scale to thousands of parallel workers on supercomputers.

### Documentation & Tutorial

My first tasks to start getting my hands on it were about refactoring the [official documentaion](https://deephyper.readthedocs.io/en/latest/) of the package and creating some of the [tutorials](https://github.com/deephyper/tutorials) that are provided there.

### Benchmarks

![List of HPOBench available benchmarks](project/deephyper/benchmarks_1.jpg "The list of available benchmarks from HPOBench. **Credit: [HPOBench](https://github.com/automl/HPOBench/wiki/Available-Containerized-Benchmarks)**")
I contributed to the development of [a framework for DeepHyper](https://github.com/deephyper/benchmark) to easily run benchmarks with specific parameters and monitor the results in a database. We used [HPOBench](https://github.com/automl/HPOBench) as a basis for our benchmarks. 

### Analytics

![The dashboard overview](project/deephyper/analytics_1.jpg "The dashboard overview.")
I developed a tool to ease the visualization of benchmarks results, easily generating diagrams and tables for comparison between benchmarks, regarding the parameters and metrics of those.

![Diagrams details](project/deephyper/analytics_2.jpg "The results of runs with the same parameters are grouped and averaged for statistical analysis ; as instance metrics like the percentage of utilization of workers (`perc_util`) can be graphed as a function of `n_jobs`.")


## Application to the Fusion Problem

Another team at ANL was working on building a detector to predict dirsuptions (instabilities) in tokamak fusion plasmas in real time before those happen[^1]. They were developing a Reccurent Deep Neural Network to process the sequential data from the different currents, fields, and temperature sensors, and output an alarm level signal that, when passing a certain threshold, would stop the reaction before the disruption happens ; they were looking for optimizing the hyperparameters of their model.

### Contribution

I entirely refectored [the code](https://github.com/deephyper/plasma-python) to make the training loop self-contained (in order for it to be compatible with BBO), as well as simpler and faster by using as much Tensorflow functions as possible. I also improved by a factor of 4 the speed of the dataloader which was initially shifting the entire array of data inputs in order to feed one batch ; I instead implemented a reading head cycling on it, and adapted the insertion of new inputs to this cycling setup.

![Search trajectory](project/deephyper/search_trajectory.png "The hyperparameter search trajectory ; each dot is a configuration.")
I then ran a BBO on [ALCF](https://www.alcf.anl.gov/)'s [ThetaGPU](https://www.alcf.anl.gov/alcf-resources/theta) to find hyperparameters configurations maximizing the AUC on the validation set, and found a lot that largely exceeded the initial configuration's performances.

![Top 80 configurations training curves](project/deephyper/top_80_training.png "Training curves of the top 80 configurations found, achieving higher AUC much faster than the baseline at training time.")

### Uncertainty Quantification

![Parallel coordinates view of the 20 best found configurations](project/deephyper/parallel_coordinates_top_20.png "Diversity of hyperparameters in the 20 best configurations found.")
The high number of different configurations generated by a BBO when ran to scale allows for ensemble prediction with a very diverse ensemble of models.

![Uncertainty quantification and prediction on a disruptive shot](project/deephyper/shot_2.png "Uncertainty quantification and prediction on a shot with a disruption at 1220ms.")
Ensemble prediction enables the estimation of the epistemic component of the uncertainty ({{< math >}}U_e{{< /math >}}), which, added to the aleatoric component ({{< math >}}U_a{{< /math >}}) depending on the average of the models' confidence, makes for a better uncertainty quantification. This was planned to be used for more accurate disruptions detection, but couldn't be studied in depth.

### Results

![ROC curve on the test set](project/deephyper/roc_curve_test.png "The ROC curve on the test set of the baseline model, best model, and best ensemble of models.")
The most notable result of this sub-project is the improvement of the ROC curve of the detector from the baseline configuration to the best model and best ensemble of models.

[^1]: Kates-Harbeck, J., Svyatkovskiy, A. & Tang, W. Predicting disruptive instabilities in controlled fusion plasmas through deep learning. _Nature_ **568**, 526–531 (2019). https://doi.org/10.1038/s41586-019-1116-4
