## Gradient-Informed Path Smoothing for Wheeled Mobile Robots (GRIPS)
[![Docker Cloud Build Status](https://img.shields.io/docker/cloud/build/icra2018/grips.svg)](https://hub.docker.com/r/icra2018/grips)
<a href="#how-to-run-with-docker"><img src="https://img.shields.io/badge/Docker-instructions-brightgreen.svg"></a>

C++ implementation of a post-smoothing approach that improves the quality of paths generated by sampling-based planners.

> Planning smooth trajectories is important for the safe, efficient and
> comfortable operation of mobile robots, such as wheeled robots moving in
> crowded environments or cars moving at high speed. Asymptotically optimal
> sampling-based motion planners can be used to generate such trajectories
> eventually. However, to achieve the necessary efficiency for the real-time
> operation of robots, one often uses their initial feasible trajectories or the
> trajectories of non-optimal planners instead, typically after a post-smoothing
> step. We propose a gradient-informed post-smoothing algorithm, called GRIPS,
> that deforms given trajectories by locally optimizing the placement of
> vertices while satisfying the system's kinodynamic constraints.  We show
> experimentally that GRIPS typically produces trajectories of significantly
> higher smoothness and smaller length than several existing post-smoothing
> algorithms.

If using GRIPS for scientific publications, please cite the following paper:

```
@inproceedings{heiden2018grips,
  author={Heiden, Eric and Palmieri, Luigi and Koenig, Sven and Arras, Kai O. and Sukhatme, Gaurav S.},
  booktitle={IEEE International Conference on Robotics and Automation (ICRA)},
  title={Gradient-Informed Path Smoothing for Wheeled Mobile Robots},
  year={2018}
}
```

## Requirements
* CMake >=3
* Eigen 3
* [OMPL ~1.3.1](https://github.com/ompl/ompl/releases)
* Qt5 (ensure the Qt Charts and SVG packages are installed)

## Content
The following CMake targets are available:

| CMake target      | Description                                                                        |
| ----------------- | ---------------------------------------------------------------------------------- |
| `homotopy_test`   | Compares paths from Theta* and A* before/after post-smoothing w.r.t homotopy class |
| `benchmark`       | Compares different post-smoothing and path planning algorithms (cf. Table 1) and generates statistics JSON in `log` folder |
| `shortening_test` | Compares path-shortening results on hand-crafted path (Fig. 2)                     |
| `showcase`        | Visualizes post-smoothing of Theta* path in S-shaped environment (Fig. 3)          |


## Used third-party tools
* [nlohmann/json](https://github.com/nlohmann/json) to store path statistics data for plotting
* [palmieri/posq](https://github.com/palmieri/posq) steer function for differential drive robots

# How to Run with Docker
## Linux
Tested on Ubuntu 16.04.6 with Docker 18.06.1-ce.

1. Open a terminal and run the command:
```
docker run --rm -p 8888:8888 -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix  icra2018/grips:latest
```
2. Run a web browser and open the link: [http://localhost:8888/lab/tree/README.ipynb](http://localhost:8888/lab/tree/README.ipynb)

## macOS
#### Prerequisites
* [XQuartz](https://www.xquartz.org/):
  - Activate the option `Allow connections from network clients` in XQuartz settings
  - Quit & restart XQuartz (to activate the setting)
  - Open a terminal and run the command:<br/> `xhost + localhost`

Tested on macOS Mojave 10.14.3 with XQuartz 2.7.11 and Docker Desktop 2.0.0.3 (engine: 18.09.2).
1. Open a terminal and run the command:
```
docker run --rm -p 8888:8888 -e DISPLAY=host.docker.internal:0 -v /tmp/.X11-unix:/tmp/.X11-unix  icra2018/grips:latest
```
2. Run a web browser and open the link: [http://localhost:8888/lab/tree/README.ipynb](http://localhost:8888/lab/tree/README.ipynb)

## Windows
### Prerequisites
* [VcXsrv](https://sourceforge.net/projects/vcxsrv/) or another X Windows Server
  - Run `Xlaunch` from the Start menu
  - Select `Multiple windows`, `Start no client`, and set `Disable access control`

Tested on Windows 10 Education wih VcXsrv 1.20.1.4 and Docker Desktop 2.0.0.3 (engine: 18.09.2).
1. Open a Windows PowerShell and run the command:
```
docker run --rm -p 8888:8888 -e DISPLAY=host.docker.internal:0  icra2018/grips:latest
```
2. Run a web browser and open the link: [http://localhost:8888/lab/tree/README.ipynb](http://localhost:8888/lab/tree/README.ipynb)
