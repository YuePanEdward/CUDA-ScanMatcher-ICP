CUDA Scan Matcher via ICP - Octree Optimized 
===============================================================================

**University of Pennsylvania, CIS 565: GPU Programming and Architecture**

Dhruv Karthik: [LinkedIn](https://www.linkedin.com/in/dhruv_karthik/)

Tested on: Windows 10 Home, Intel(R) Core(TM) i7-8700 CPU @ 3.20GHz, 16GM, GTX 2070 - Compute Capability 7.5
____________________________________________________________________________________
![Developer](https://img.shields.io/badge/Developer-Dhruv-0f97ff.svg?style=flat) ![CUDA 10.1](https://img.shields.io/badge/CUDA-10.1-yellow.svg) ![Built](https://img.shields.io/appveyor/ci/gruntjs/grunt.svg) ![Issues](https://img.shields.io/badge/issues-none-green.svg)
____________________________________________________________________________________
<p align="center">
  <img  src="img/waymotrue.gif">
</p>

Table of contents
=================
   * [Scan Matching Algorithm](#scan-matching-algorithm)
  * [Optimizations](#optimizations)
    * [Stream compaction to remove terminated rays](#stream-compaction-to-remove-terminated-rays)
    * [First bounce caching](#first-bounce-caching)
    * [Sort by Material](#sort-by-material)
   * [Questions](#questions)
   * [Performance Analysis](#performance-analysis)
   * [Credits & Acknowledgments](#credits)
   
# Scan Matching Algorithm
Scan Matching seeks to align two similar pointclouds by finding the transformation between them. It does so via the iterative closest point algorithm outlined below pseudocode:
```bash
#Aligns pointcloud A to pointcloud B
def scan_match(pointcloud A, pointcloud B):
  1. For each point in A, find the closest point in B
  2. Compute a 3-D transformation matrix that aligns the points (Use SVD & Least Squares Regression)
  3. Update all points in the target by the transformation matrix
  4. Repeat steps 1-3 until some epsilon convergence
  RETURN : Some Transformation matrix T
```
