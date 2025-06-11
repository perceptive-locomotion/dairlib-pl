# dairlib-pl
This repo contains the code for "Perceptive Mixed-Integer Footstep Control for Underactuated Bipedal Walking on Rough Terrain" by [Brian Acosta](https://github.com/Brian-Acosta) and [Michael Posa](https://github.com/mposa). The code is based on [dairlib](https://github.com/DAIRLab/dairlib). We have separated the perceptive locomotion project into this dedicated fork due to the need for several additional external dependencies compared to a baseline dairlib installation.   

### Download dairlib-pl
1. Clone `dairlib-pl` into the your workspace, e.g. "my-workspace/dairlib-pl".
```
git clone https://github.com/perceptive-locomotion/dairlib-pl.git
```

2. Download and setup SNOPT

dairlib, by default, assumes that users have access to SNOPT(https://web.stanford.edu/group/SOL/snopt.htm), though it is not required. **If you do not have SNOPT**, you will need to edit `.bazelrc` and change `build --define=WITH_SNOPT=ON` to `build --define=WITH_SNOPT=OFF`

For users at Penn, download SNOPT (https://www.seas.upenn.edu/~posa/snopt/snopt7.6.tar.gz) and add the following line to your `~/.bashrc`
```
export SNOPT_PATH=<the directory you downloaded to>/snopt7.6.tar.gz
```

There is no need to extract the tar.

3. Download and setup Gurobi

The mixed-integer footstep controller uses the commercially licensed Gurobi solver. Follow the [drake gurobi installation instructions](https://drake.mit.edu/bazel.html#gurobi-100) to set up gurobi. 



### Build Drake
The library is meant to be built with Drake (see http://drake.mit.edu/ for more details). There are two ways to use Drake within dairlib:

#### Option 1: use pegged revision (Note - These steps may need repeated if switching to a branch with a different pegged revision of drake).
The only specific action needed here is to install all of Drake's prerequisites. There are two choices for completing this step:

a) In `dairlib/install`, run the appropriate `install_prereqs_xxx.sh`. This is untested on mac, and has not been tested to get every dependency for a fresh install.

b) Download a source copy of drake, and install pre-requisites as described here: http://drake.mit.edu/from_source.html. Drake dependencies can change without notice. For full compatiability, you may need to checkout the drake commit which is pegged in WORKSPACE to install the correct dependencies. There is no need to build Drake itself. Proceed only until you have run the Drake setup script. 

bazel will automatically download the pegged revision, specified in the WORKSPACE file. dairlib developers hope to keep this pegged revision current, and ensure that the pegged version will always work with a specific version of dairlib.

This option is recommended for users who are not currently editing any source code in Drake itself.

#### Option 2: source install of Drake
Complete both steps (a) and (b) above. By running the drake install script after the dairlib install script, you are capturing any dependency changes between the pegged revision and the current Drake master, while still getting any aditional dairlib dependencies we may add. There is no need to build Drake. Next, to tell dairlib to use your local install, set the environment variable `DAIRLIB_LOCAL_DRAKE_PATH`, e.g.
```
export DAIRLIB_LOCAL_DRAKE_PATH=/home/user/my-workspace/drake
```

### Other dependencies
These dependencies are necessary for some advanced visualization and process management. Many examples will work without a full installation of Director or libbot, but these are ultimately recommended. 

#### LCM and libbot
Install a local copy of `lcm` and `libbot2` using `sudo apt install lcm libbot2`. The prerequisites installation (option 1.a) should add the proper apt repo for these.

### Build dairlib
Build what you want via Bazel. From `dairlib`,  `bazel build ...` will build the entire project. Drake will be built as an external dependency.
- If you run into ram/cpu limits while building, you can cap the number of threads bazel will use (here we choose `8`) by either:
    - adding `build --jobs=8` to `.bazelrc` 
    - using the `jobs` flag when calling `build` (e.g. `bazel build [target] --jobs=8`)
