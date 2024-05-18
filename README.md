# Self-Learning RLHF

Official implementation of the paper: "Self-Learning Enhanced RLHF: Integrating Task Objectives for Improved Performance in Different Tasks". Our implementation is based on the official codebase of [MRN](https://github.com/RyanLiu112/MRN), [B-Pref](https://github.com/rll-research/BPref) and [SURF](https://github.com/alinlab/SURF).

This is only for the Meta-world. There is different SL-RLHF Framework for DMControl. However, it is still recommended to completely install the conda environment of SlRlhf, because this environment is common to both DMControl and Meta world. If you have any problems with installation, you can first check the install_problem.md file

## How to install

### Install MuJoCo 2.0

```bash
sudo apt update
sudo apt install unzip gcc libosmesa6-dev libgl1-mesa-glx libglfw3 patchelf libegl1 libopengl0
sudo ln -s /usr/lib/x86_64-linux-gnu/libGL.so.1 /usr/lib/x86_64-linux-gnu/libGL.so
wget https://www.roboti.us/download/mujoco200_linux.zip -P /tmp
unzip /tmp/mujoco200_linux.zip -d ~/.mujoco
wget https://www.roboti.us/file/mjkey.txt -P /tmp
mv /tmp/mjkey.txt ~/.mujoco/
```

### Install dependencies

```bash
conda env create -f conda_env.yml
conda activate SlRlhf
pip install -e .[docs,tests,extra]
cd custom_dmcontrol
pip install -e .
cd ../custom_dmc2gym
pip install -e .
cd ..
pip install git+https://github.com/rlworkgroup/metaworld.git@04be337a12305e393c0caf0cbf5ec7755c7c8feb
pip install pybullet termcolor
```



## How to run

### Meta-world (Door Open)
#### SAC

```bash
python train_SAC.py env=metaworld_door-open-v2 seed=12345 agent.params.actor_lr=0.0003 agent.params.critic_lr=0.0003 num_unsup_steps=9000 num_train_steps=1000000 agent.params.batch_size=512 double_q_critic.params.hidden_dim=256 double_q_critic.params.hidden_depth=3 diag_gaussian_actor.params.hidden_dim=256 diag_gaussian_actor.params.hidden_depth=3
```

#### MRN

```bash
python train_MRN.py env=metaworld_door-open-v2 seed=12345 agent.params.actor_lr=0.0003 agent.params.critic_lr=0.0003 num_unsup_steps=9000 num_train_steps=1000000 agent.params.batch_size=512 double_q_critic.params.hidden_dim=256 double_q_critic.params.hidden_depth=3 diag_gaussian_actor.params.hidden_dim=256 diag_gaussian_actor.params.hidden_depth=3 num_interact=5000 max_feedback=1000 reward_batch=10 reward_update=10 feed_type=1 num_meta_steps=10000
```
#### MRN_self

```bash
python train_MRN_self.py env=metaworld_door-open-v2 seed=12345 agent.params.actor_lr=0.0003 agent.params.critic_lr=0.0003 num_unsup_steps=9000 num_train_steps=1000000 agent.params.batch_size=512 double_q_critic.params.hidden_dim=256 double_q_critic.params.hidden_depth=3 diag_gaussian_actor.params.hidden_dim=256 diag_gaussian_actor.params.hidden_depth=3 num_interact=5000 max_feedback=1000 reward_batch=10 reward_update=10 feed_type=1 num_meta_steps=10000 self_frequency=1000
```

#### PEBBLE

```bash
python train_PEBBLE.py env=metaworld_door-open-v2 seed=12345 agent.params.actor_lr=0.0003 agent.params.critic_lr=0.0003 num_unsup_steps=9000 num_train_steps=1000000 agent.params.batch_size=512 double_q_critic.params.hidden_dim=256 double_q_critic.params.hidden_depth=3 diag_gaussian_actor.params.hidden_dim=256 diag_gaussian_actor.params.hidden_depth=3 num_interact=5000 max_feedback=1000 reward_batch=10 reward_update=10 feed_type=1
```
#### PEBBLE_self

```bash
python train_PEBBLE_self.py env=metaworld_door-open-v2 seed=12345 agent.params.actor_lr=0.0003 agent.params.critic_lr=0.0003 num_unsup_steps=9000 num_train_steps=1000000 agent.params.batch_size=512 double_q_critic.params.hidden_dim=256 double_q_critic.params.hidden_depth=3 diag_gaussian_actor.params.hidden_dim=256 diag_gaussian_actor.params.hidden_depth=3 num_interact=5000 max_feedback=1000 reward_batch=10 reward_update=10 feed_type=1 self_frequency=1000
```

#### SURF

```bash
python train_PEBBLE_semi_dataaug.py env=metaworld_door-open-v2 seed=12345 agent.params.actor_lr=0.0003 agent.params.critic_lr=0.0003 num_unsup_steps=9000 num_train_steps=1000000 agent.params.batch_size=512 double_q_critic.params.hidden_dim=256 double_q_critic.params.hidden_depth=3 diag_gaussian_actor.params.hidden_dim=256 diag_gaussian_actor.params.hidden_depth=3 num_interact=5000 max_feedback=1000 reward_batch=10 reward_update=20 feed_type=1 inv_label_ratio=10 threshold_u=0.99 mu=4
```
#### SURF_self

```bash
python train_PEBBLE_semi_dataaug_self.py env=metaworld_door-open-v2 seed=12345 agent.params.actor_lr=0.0003 agent.params.critic_lr=0.0003 num_unsup_steps=9000 num_train_steps=1000000 agent.params.batch_size=512 double_q_critic.params.hidden_dim=256 double_q_critic.params.hidden_depth=3 diag_gaussian_actor.params.hidden_dim=256 diag_gaussian_actor.params.hidden_depth=3 num_interact=5000 max_feedback=1000 reward_batch=10 reward_update=20 feed_type=1 inv_label_ratio=10 threshold_u=0.99 mu=4 self_frequency=1000
```



## Citation

```
@inproceedings{hu2024slrlhf,
  title={SelfLearning-RLHF},
  author={Jiabin Hu and Xiaoyi Wei and Peng Zhai and Lihua Zhang},
}
```

