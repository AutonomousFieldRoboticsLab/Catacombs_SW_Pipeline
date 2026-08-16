# Catacombs_SW_Pipeline
The following instruction will allow a user to setup the software pipeline for mapping an underwater cave. The main packages involved are:

- GoProRos [1]: software for converting GoPro video files into ROS2 bag files
- SVIn2 [2]: A Visual Inertial SLAM package based on Okvis [3].
- Colmap [4]: A shape from motion package for global optimization and dense reconstruction

## GoProRos:
Follow the installation instructions at:

It is possible you will need to install the following libraries separately:
```
sudo apt install libpostproc-dev
sudo apt-get install libavdevice-dev
sudo apt-get install libavfilter-dev
```

## SVIn:

## Colmap:

### Citations:
The above pipeline is based on the following publications:
```
[1] @inproceedings{JoshiICRA2022,
    author = {Bharat Joshi and Marios Xanthidis and Sharmin Rahman and Ioannis Rekleitis},
    booktitle = {IEEE International Conference on Robotics and Automation (ICRA)},
    title = {High Definition, Inexpensive, Underwater Mapping},
    year = {2022},
    pages = {1113-1121},
    doi = {10.1109/ICRA46639.2022.9811695}
}
[2] @article{RahmanIJRR2022,
    author = {Sharmin Rahman and Alberto {Quattrini Li}  and Ioannis Rekleitis},
    booktitle = {},
    title = {SVIn2: A Multi-sensor Fusion-based Underwater SLAM System},
    year = {2022},
    volume = {41},
    number = {11-12},
    pages = {1022-1042},
    doi = {10.1177/02783649221110259}
}
[3] @article{leutenegger2015keyframe,
    title={Keyframe-based visual--inertial odometry using nonlinear optimization},
    author={Leutenegger, Stefan and Lynen, Simon and Bosse, Michael and Siegwart, Roland and Furgale, Paul},
    journal={The International Journal of Robotics Research},
    volume={34},
    number={3},
    pages={314--334},
    year={2015},
    publisher={SAGE Publications Sage UK: London, England}
}
[4] @inproceedings{schonberger2016structure,
    title={Structure-from-motion revisited},
    author={Schonberger, Johannes L and Frahm, Jan-Michael},
    booktitle={Proceedings of the IEEE conference on computer vision and pattern recognition},
    pages={4104--4113},
    year={2016}
}


```
