### Vision-aided walking on Cassie

This folder contains the controller binaries for vision-aided walking on Cassie.
It also contains some of the C++ libraries necessary for the perception modules, 
which have python entry points located in `bindings/pydairlib/perceptive_locomotion`. 

The scripts in this folder use LCM for inter-process communication and are 
designed for deployment on a real robot. 

For deterministic simulations, where the components pass information directly 
through the drake systems framework, see `bindings/pydairlib/perceptive_locmotion/sim_experiments` 

### Running the scripts
We use the process manager, bot-procman (https://github.com/libbot2/libbot2/tree/master/bot2-procman), 
to organize the scripts. To use procman, use the command
`bot-procman-sheriff -l examples/perceptive_locomotion/alip_mpfc_simulation.pmd`. 
Another option is to simply run the compiled binaries located in `bazel-bin`.

Note that procman expects the binaries to be present in `baze;-bin/`, requiring 
the examples to have been built using `bazel build examples/perceptive_locomotion/...`
before running the scripts.


### Read about the methods implemented here

Papers: http://arxiv.org/abs/2309.07993, https://arxiv.org/pdf/2501.19391

Recommended citation: 

```
@article{Acosta2025,
  title = {Perceptive Mixed-Integer Footstep Control for Underactuated Bipedal Walking on Rough Terrain},
  author = {Acosta, Brian and Posa, Michael},
  year = {2025},
  month = jan,
  journal = {IEEE Transactions on Robotics},
  arxiv = {2501.19391},
  youtube = {JK16KJXJxi4},
  doi = {10.1109/TRO.2025.3587998},
  url = {https://ieeexplore.ieee.org/document/11077715}
}
```