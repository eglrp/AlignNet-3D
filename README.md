## Installation

- Install Tensorflow (tested with version 1.8.0)
- Clone Open3D fork from [https://github.com/grossjohannes/Open3D](https://github.com/grossjohannes/Open3D)
- Build Open3D, build and install the Open3D python package (see [http://www.open3d.org/docs/compilation.html](http://www.open3d.org/docs/compilation.html))

## Dataset preparation

- Download the datasets:
  - [Synth20.zip](https://drive.google.com/uc?id=1BJIJIv0p8lbLihK38YNjtqCGfJYO3fSK&export=download)
  - [Synth20others.zip](https://drive.google.com/uc?id=1TX7nW-WqV6MfYBcWZbG6plAHmeeWdxHS&export=download)
  - [SynthCars.zip](https://drive.google.com/uc?id=1Iw-tZJF-dDzKLigkZDY6WZI4S1g80t7g&export=download)
  - [SynthCarsPersons.zip](https://drive.google.com/uc?id=1RDM7taNl4RGWaj9eEdYrnOfPyP7Jk0ts&export=download)
  - [KITTITrackletsCars.zip](https://drive.google.com/uc?id=1b_9n_xXSAxOSii4QZsjWu-HS0AiXvtvG&export=download)
  - [KITTITrackletsCarsPersons.zip](https://drive.google.com/uc?id=1HF4PFUefYT3KOh9l5E4dKbIyiycMV8Tl&export=download)
  - [KITTITrackletsCarsHard.zip](https://drive.google.com/uc?id=110HGSTa7X-pTK0rYA4w9bEICjmfvgF2-&export=download)
  - [KITTITrackletsCarsPersonsHard.zip](https://drive.google.com/uc?id=12f58V5aQIx2w2YPuetOQrnRyCLBFOnsh&export=download)
- Extract the datasets to the same directory, e.g. `/home/gross/data`.  The folder structure should look like

```
data
│
└───SynthCars
│   │
│   └───meta
│   │   │   00000000.json
│   │   │   00000001.json
│   │   │   ...
│   │
│   └───pointcloud1
│   │   │   00000000.npy
│   │   │   00000001.npy
│   │   │   ...
│   │
│   ...
│
└───SynthCarsPersons
    │   ...
```

## Running ICP evaluations

- Specify your dataset folder (e.g. `/home/gross/data`) in make_icp_configs.py
- Prepare the icp configs by running `python make_icp_configs.py`
- Run all icp evaluations at once with `./eval_icp.sh`

## Training

- Adapt _logging.basedir_ in `configs/default.json`
- Run e.g. `python train.py --config configs/SynthCars.json`
- Models and evaluation results will be written to the specified _logging.basedir_
- For models with pre-training from other models, adapt _training.pretraining.model_ in the respective config files (e.g. `configs/KITTITrackletsCars.json`)

## Evaluation

- To run evaluation (again) with an existing model checkpoint, run e.g. `python train.py eval_only --config configs/KITTITrackletsCarsHard.json --eval_epoch 28`
- To run evaluation (again) with inference outputs (pred_translations.npy, pred_angles.npy, ...), run e.g. `python train.py eval_only --config configs/KITTITrackletsCarsHard.json --eval_epoch 28 --use_old_results`
- To run evaluation (again) with ICP refinement, run e.g. `python train.py eval_only --config configs/KITTITrackletsCarsHard.json --eval_epoch 28 --refineICP --use_old_results`
- Some trained models and evaluation results can be found in [models_alignnet.zip](https://drive.google.com/open?id=1byWj8J73fHTBSkXL2qOrPojSMhENP7SQ)

## References

- This repository builds upon, thus borrows code heavily from [PointNet](https://github.com/charlesq34/pointnet), [Frustum PointNets](https://github.com/charlesq34/frustum-pointnets) and [DGCNN](https://github.com/WangYueFt/dgcnn).
