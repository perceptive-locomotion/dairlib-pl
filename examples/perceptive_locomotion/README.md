## Vision-aided walking on Cassie

This folder contains the controller binaries for vision-aided walking on Cassie.
It also contains some of the C++ libraries necessary for the perception modules, 
which have python entry points located in `bindings/pydairlib/perceptive_locomotion`. 

The scripts in this folder generally use LCM for inter-process communication and are 
designed for deployment on a real robot. For deterministic simulations, see
`standalone_experiment_sim` for a basic implementation and `bindings/pydairlib/perceptive_locmotion/sim_experiments` 
for more sophisticated examples, including full-stack perception. 

## Running the scripts
We use the process manager, bot-procman (https://github.com/libbot2/libbot2/tree/master/bot2-procman), 
to organize the scripts. To use procman, use the command
`bot-procman-sheriff -l examples/perceptive_locomotion/alip_mpfc_simulation.pmd`. 
Another option is to simply run the compiled binaries located in `bazel-bin`.

Note that procman expects the binaries to be present in `bazel-bin/`, requiring 
the examples to have been built using `bazel build examples/perceptive_locomotion/...`
before running the scripts.

### Included Scripts 

- `cassie_perception_visualizer` visualizes the elevation map which is being published on a user-specified channel. 
- `mpc_visualizer` visualizes the foothold and footstep solutions from MPFC.
- `multibody_sim_hiking` runs the drake simulation. To use the ground-truth terrain, ensure that the terrain yaml arguments match for the simulator and mpfc binaries.
- `run_alip_s2s_mpfc_controller` runs the mixed-integer footstep controller
- `run_controller_switch` listens to the MPFC contact switching messages in order to switch to walking during a nominal double stance period. 
- `run_osc_for_alip_mpfc_controller` runs the operational space controller to realize MPFC footstep plans on Cassie.
- `standalone_experiment_sim` runs a deterministic full simulation with the walking controller and dynamics simulation in a single process, using ground-truth state and terrain information. 

### Other goodies

- See `diagrams/cassie_realsense_driver_diagram` for a drake diagram which directly polls the realsense in the same process as elevation mapping, in order to minimize latency and network traffic.

## Read about the methods implemented here

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