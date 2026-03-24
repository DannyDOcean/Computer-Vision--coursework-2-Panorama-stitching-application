# Computer Vision – Coursework 2: Panorama Stitching

## Overview
This project builds a panorama stitching tool entirely from scratch in Python. I only use OpenCV for loading images and SIFT; everything else runs on custom code. The app takes two overlapping photos and merges them into one seamless panorama.

## How to Run
Make sure you have numpy, opencv-python, and scipy installed:
```
pip install numpy opencv-python scipy
python cw2.py
```
Place `s1.jpg` and `s2.jpg` alongside `cw2.py` in the same directory.

## Pipeline
1. **Feature Detection** – SIFT locates keypoints and grabs descriptors from both images.
2. **Feature Matching** – A homemade brute-force matcher pairs features using Lowe’s ratio test (set at 0.75).
3. **Match Visualization** – The script connects corresponding features in both images and saves the result as `matches.jpg`.
4. **Homography Estimation** – RANSAC (2000 rounds) finds the best transformation matrix via a custom DLT solver.
5. **Warping & Stitching** – Inverse warping maps both images onto a common canvas, taking care of translation between them.
6. **Linear Blending** – The overlap zone uses feathered blending for a smooth, natural look.
7. **Black Border Removal** – The final image crops out empty regions, keeping only the actual content.

## Output
- `panorama_result.jpg` is your finished panorama.
- `matches.jpg` shows matched keypoints between the original images.

## Group Members & Responsibilities
| Member    | Section                                              |
|-----------|------------------------------------------------------|
| Danny     | Feature matching, RANSAC, DLT homography, warping    |
                                     |

## Notes
- All algorithms for stitching, RANSAC, and homographies are built from scratch, no OpenCV shortcuts.
- DLT code reuses methods from Coursework 1.
- Blending options include both linear feathering and Laplacian pyramid multiband blending.
