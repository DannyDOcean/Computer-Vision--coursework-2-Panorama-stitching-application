# Computer Vision – Coursework 2: Panorama Stitching

## Overview
This project implements a panorama stitching application from scratch in Python using OpenCV (for image I/O and SIFT only). Two overlapping images are automatically stitched into a single wide panorama.

## How to Run
```bash
pip install numpy opencv-python scipy
python cw2.py
```
Make sure `s1.jpg` and `s2.jpg` are in the same folder as `cw2.py`.

## Pipeline
1. **Feature Detection** – SIFT keypoints and descriptors extracted from both images
2. **Feature Matching** – Custom brute-force matcher with Lowe's ratio test (threshold = 0.75)
3. **Match Visualisation** – Correspondences drawn between images and saved as `matches.jpg`
4. **Homography Estimation** – Custom RANSAC (2000 iterations) with custom DLT solver
5. **Warping & Stitching** – Inverse warping onto shared canvas with translation offset
6. **Linear Blending** – Feathering across the overlap region for smooth transition
7. **Black Border Removal** – Bounding box crop of non-black content

## Output
- `panorama_result.jpg` – Final stitched panorama
- `matches.jpg` – Visualised feature matches between input images

## Group Members & Responsibilities
| Member | Section |
|--------|---------|
| Danny  | Feature matching, RANSAC, DLT homography, warping |
| *Member 2* | *Update this* |
| *Member 3* | *Update this* |

## Notes
- No OpenCV stitching, RANSAC, or homography methods used — all implemented from scratch
- DLT algorithm reused from Coursework 1
- Blending implemented as both linear (feathering) and multiband (Laplacian pyramid)
