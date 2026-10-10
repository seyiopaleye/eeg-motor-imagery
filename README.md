# eeg-motor-imagery


Classifying imagined left- vs right-hand movement from EEG using Python, MNE and scikit-learn.

![Power spectra at C3 and C4 for imagined left vs right hand movement](result_figure.png)

## Summary

This project asks whether a computer can tell if someone is imagining moving their left or right hand, using only scalp EEG. This is the core idea behind many brain-computer interfaces (BCIs). I used open-access data from one subject in the PhysioNet EEG Motor Movement/Imagery dataset, filtered it to the mu and beta bands (8–30 Hz), cut it into trials, and trained a CSP + LDA classifier.

The cross-validated accuracy was **0.66 ± 0.17**, against a chance level of **0.51** (the classes are almost perfectly balanced: 23 left and 22 right trials). This is above chance, but the large standard deviation and small number of trials mean the estimate is uncertain. I treat it as a promising result for one subject, not a reliable measure of performance.

## Dataset

- PhysioNet EEG Motor Movement/Imagery Dataset, loaded with `mne.datasets.eegbci`
- Subject 1, runs 4, 8 and 12 (imagining opening and closing the left or right fist)
- 64 EEG channels, sampled at 160 Hz
- 45 trials in total (23 left, 22 right)

## Method

1. **Load** the three runs and join them into one recording.
2. **Band-pass filter** at 8–30 Hz, the range containing the mu (8–12 Hz) and beta (13–30 Hz) rhythms, which change during movement and imagined movement.
3. **Epoch** from 1 s before to 4 s after each cue, labelled left or right.
4. **Visualise** the power spectrum at C3 and C4, two electrodes over the left and right motor cortex.
5. **Classify** using the 1–2 s after the
