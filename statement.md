# Project Statement

## Problem Statement
Estimating scene depth from images is a core problem in computer vision, with applications ranging from robotics and autonomous navigation to 3D reconstruction and augmented reality. Traditional single-camera (monocular) systems cannot directly recover depth without additional cues, while fully calibrated multi-camera systems require precise knowledge of camera intrinsics and extrinsics that is often unavailable in practice.

This project addresses the problem of estimating **relative scene depth from a pair of stereo images when camera calibration parameters are not known**. Given two images of the same scene captured from slightly different viewpoints, the goal is to recover the geometric relationship between the views, correct for their misalignment, and compute a disparity map that reflects the relative depth structure of the scene — all without relying on metric calibration data.

## Scope of the Project
The project is scoped as a classical (non-deep-learning) computer vision pipeline built around feature matching, epipolar geometry, and dense stereo matching. Specifically, it covers:

- **In scope:**
  - Detecting and matching keypoints (ORB features) across stereo image pairs
  - Estimating the fundamental matrix using RANSAC-based robust fitting
  - Visualizing epipolar lines to illustrate the geometric relationship between views
  - Computing dense disparity maps using two methods: SGBM and NCC
  - Performing **uncalibrated** stereo rectification from point correspondences (no known camera intrinsics)
  - Qualitatively and visually comparing disparity maps before and after rectification

- **Out of scope:**
  - Metric (absolute-unit) depth or 3D reconstruction, since camera intrinsics/baseline are not used
  - Calibrated stereo pipelines requiring known camera parameters
  - Deep learning–based stereo matching or depth estimation methods
  - Real-time or video-based stereo processing
  - Quantitative benchmarking against ground-truth depth datasets (identified only as a future improvement)

## Target Users
- **Students and learners** studying computer vision, who want a clear, well-structured reference implementation of classical stereo vision concepts (feature matching, epipolar geometry, rectification, disparity estimation)
- **Educators/instructors** looking for a portfolio-style example project to illustrate stereo vision theory with concrete code and visual outputs
- **Computer vision practitioners/researchers** who need a lightweight, dependency-minimal baseline for experimenting with uncalibrated stereo techniques before moving to calibrated or learning-based approaches
- **Portfolio reviewers/recruiters** evaluating the author's understanding of classical computer vision techniques through a documented, reproducible project

## High-Level Features
- **Feature detection and matching**: ORB keypoint detection with brute-force Hamming-distance descriptor matching across stereo pairs
- **Fundamental matrix estimation**: Robust estimation via RANSAC to filter outlier correspondences
- **Epipolar geometry visualization**: Drawing and displaying epipolar lines on matched image pairs to illustrate the underlying geometric constraints
- **Dense disparity computation**: Two interchangeable stereo matching algorithms —
  - SGBM (Semi-Global Block Matching) for smoother, more robust disparity maps
  - NCC (Normalized Cross-Correlation) as a simpler local baseline
- **Uncalibrated stereo rectification**: Homography-based rectification derived purely from point correspondences, without camera intrinsics
- **Before/after comparison**: Side-by-side qualitative comparison of epipolar alignment and disparity quality before and after rectification
- **Modular codebase**: Separated modules for geometry, I/O, rectification, stereo matching, and visualization (`src/pcv/`), with two runnable entry-point scripts (`run_part1.py`, `run_part2.py`) producing organized outputs
