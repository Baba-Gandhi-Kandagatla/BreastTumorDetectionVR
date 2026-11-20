# Breast ultrasound classification and segmentation

## Introduction

A research prototype for classifying breast ultrasound images and localizing masses with segmentation masks.

## Tech stack

Python with PyTorch, TensorFlow/Keras and OpenCV for model experiments and inference. Flask exposes prediction services. A React client and an Express account service provide the web interface. The broader project used Unreal Engine for visualization.

## Features

- Predict benign, malignant or normal classes for ultrasound images or video frames.
- Segment a mass and inspect the mask alongside the ultrasound.
- Review per-image F1, Jaccard, recall and precision in the evaluation table.

## The process

| Task | Models and evidence |
| --- | --- |
| Classification | `MERN/app.py` contains ViT-B/16 and EfficientNetB0 inference paths for images and video. `efficient-net-final.ipynb` contains the EfficientNet experiment. |
| Segmentation | `unetr-b.ipynb` and `unet/unet-final.ipynb` contain the UNETR and U-Net experiments. The `unet/` directory includes example input, mask and prediction videos. |
| Evaluation | `unet/score.csv` records per-image F1, Jaccard, recall and precision. Its rows let readers inspect variation across examples. |
| Visualization | The broader project incorporated Unreal Engine visualization. `test.py` shows the Python side streaming image or video frames over a local WebSocket. The Unreal project assets are separate from this checkout. |

Some filenames, routes and older screenshots use “LLM” for the transformer path. The classifier behind that label is a vision transformer operating on ultrasound imagery.

## How it can be improved

A versioned manifest of dataset splits, preprocessing settings and checkpoint identifiers would help readers connect a notebook run to its prediction outputs and score table.

## How to run

To explore the saved results, open the [per-image score table](unet/score.csv) or [U-Net experiment](unet/unet-final.ipynb). To start the web client from the repository root:

```sh
cd MERN/client
npm ci
npm run dev
```

The inference services require trained checkpoints, including the ViT weights, EfficientNet weights and a Keras segmentation model referenced in `MERN/app.py`. Those files need to be supplied separately. The repository also includes a React client under `MERN/client/`, an Express account service under `MERN/server/`, and a separate Flask segmentation service in `MERN/dlapp.py`.

The evaluation table reports experimental results on the project data. It does not establish clinical performance.

## Screenshots

![Example ultrasound image, corresponding binary mass mask and overlay.](docs/images/segmentation-example.png)

From left to right: source ultrasound, binary mask and overlay.
