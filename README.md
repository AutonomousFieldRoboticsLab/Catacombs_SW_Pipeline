# Catacombs_SW_Pipeline
The following instruction will allow a user to setup the software pipeline for mapping an underwater cave. The main packages involved are:

- GoProRos [1]: software for converting GoPro video files into ROS2 bag files
- SVIn2 [2]: A Visual Inertial SLAM package based on Okvis [3].
- Colmap [4]: A shape from motion package for global optimization and dense reconstruction
## Installation
### GoProRos2:
Follow the installation instructions at:
```
https://github.com/AutonomousFieldRoboticsLab/gopro_ros2
```

### SVIn:
Follow the installation instructions at:
https://github.com/AutonomousFieldRoboticsLab/SVIn/blob/main/install.md


### Svin-Perdix-Matcher:
```
mkdir ~/depth_matcher_ws
cd ~/depth_matcher_ws
git clone https://github.com/AutonomousFieldRoboticsLab/Svin-Perdix-Matcher .
sudo apt install python3-venv
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install -r requirements.txt
```

### Colmap:
---
## Usage

### GoProRos2
In order to convert a GoPro video file into a ROS2 bag file you will need to have two directories (one for the video files and one for the bag file) for example:
```
~/Desktop/Catacombs/Videos/Center/
~/Desktop/Catacombs/ros2bags/center_bag
```

Then run the following command(s):

For a sequence of videos saved inside a directory (please note, ~ is not always recognized, so replace with the full path):
```
ros2 launch gopro_ros2 gopro_to_rosbag.xml gopro_folder:=~/Desktop/Catacombs/Videos/Center/ multiple_files:=true rosbag:=~/Desktop/Catacombs/ros2bags/center_bag
```
For a single video:
```

```
The above instruction will save gray-scale images. For color images see the section on extracting keyframes. 

### SVIn:
Run the launch file for GoPro 9:

```bash
source install/setup.bash
ros2 launch okvis_ros svin_gopro_uw.xml
```
In different terminal, run the bag file

```bash
source /opt/ros/jazzy/setup.bash
ros2 bag play ~/Desktop/Catacombs/ros2bags/center_bag --clock
```
To save the trajectory:
```
ros2 service call /save_trajectory std_srvs/srv/Trigger {}
```
Trajectory is saved at 
```
~/svin_ws/src/SVIn/pose_graph/svin_results
```
To save the pointcloud:
```
ros2 service call /save_pointcloud std_srvs/srv/Trigger {}
```

Pointcloud is saved at:
```
~/svin_ws/src/SVIn/pose_graph/reconstruction_results
```

To transform to real water depth from a dive computer:
```bash
cd ~/depth_matcher_ws
source .venv/bin/activate
python3 svin_perdix_matcher.py ~/Desktop/Catacombs/Perdix/CatacombsPerdix.csv ~/svin_ws/src/SVIn/pose_graph/svin_results/<svin_2026_file.txt> <output_path> {m|ft} --pointcloud ~/svin_ws/src/SVIn/pose_graph/reconstruction_results/<svin_2026_file.ply>
```
Please note: the matcher uses data from the dive computer in ft or meters {m|ft}.
Please note: the matcher reports several images as described in the paper together with the adjusted trajectory
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
