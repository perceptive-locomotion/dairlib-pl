# dairlib-pl

#### NOTE: Code-cleanup is in-progress, including instructions for running the perceptive locomotion examples 

This repo contains the code for "Perceptive Mixed-Integer Footstep Control for 
Underactuated Bipedal Walking on Rough Terrain" by 
[Brian Acosta](https://github.com/Brian-Acosta) and 
[Michael Posa](https://github.com/mposa). 
The code is based on [dairlib](https://github.com/DAIRLab/dairlib). 
We have separated the perceptive locomotion project into this dedicated fork due
to the need for several additional external dependencies compared to a baseline 
dairlib installation.

In addition to the installation instructions below, you will need the following 
dependencies (installed through your system's package manager):

- OpenCV
- librealsense2 (MacOS only - bazel will handle this for you on ubuntu)

And then following python modules:
- scipy
- TODO

#### See examples/perceptive_locomotion for instructions on running the examples

### Download and install dairlib-pl
1. Install dependencies

This repo is based heavily on [Drake](drake.mit.edu). 
To install the drake dependencies, before downloading dairlib, download drake and run the prerequisite script:  
```
git clone --depth 1 --branch v1.35.0 https://github.com/RobotLocomotion/drake.git
sudo drake/setup/ubuntu/install_prereqs.sh
```

You can delete this copy of Drake once the prereq script has successfully finished.

2. Clone `dairlib-pl` into your workspace, e.g. "my-workspace/dairlib-pl".
```
git clone https://github.com/perceptive-locomotion/dairlib-pl.git
```

3. Download and setup SNOPT

dairlib, by default, assumes that users have access to SNOPT(https://web.stanford.edu/group/SOL/snopt.htm), though it is not required. **If you do not have SNOPT**, you will need to edit `.bazelrc` and change `build --define=WITH_SNOPT=ON` to `build --define=WITH_SNOPT=OFF`

For users at Penn, download SNOPT (https://www.seas.upenn.edu/~posa/snopt/snopt7.6.tar.gz) and add the following line to your `~/.bashrc`
```
export SNOPT_PATH=<the directory you downloaded to>/snopt7.6.tar.gz
```

There is no need to extract the tar.

4. Download and setup Gurobi

The mixed-integer footstep controller uses the commercially licensed Gurobi solver. 
Follow the [drake gurobi installation instructions](https://drake.mit.edu/bazel.html#gurobi-100) to set up gurobi.

### Other dependencies
These dependencies are necessary for some advanced visualization and process 
management. Many examples will work without a full installation of Director 
or libbot, but these are ultimately recommended. 

LCM is necessary for running the perceptive locomotion simulations, 
which write LCM logs to disk after the simulation concludes 

#### LCM and libbot
Install a local copy of `lcm` and `libbot2` using `sudo apt install lcm libbot2`. The prerequisites installation (option 1.a) should add the proper apt repo for these.

### Build dairlib
Build what you want via Bazel. From `dairlib`,  `bazel build ...` will build the entire project. Drake will be built as an external dependency.
- If you run into ram/cpu limits while building, you can cap the number of threads bazel will use (here we choose `8`) by either:
    - adding `build --jobs=8` to `.bazelrc` 
    - using the `jobs` flag when calling `build` (e.g. `bazel build [target] --jobs=8`)
