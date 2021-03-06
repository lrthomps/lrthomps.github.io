---
layout: post
title:  "GPU for ML only on Ubuntu"
tags: ["other"]
date:   2020-09-11
summary: To go against the grain, you have to fight. 


---


I fought with NVIDIA drivers taking over my graphics and xterm on Ubuntu 20.04. It was either have my GPU do everything and lose up to half its memory in the process... or nothing. I had it working once... then updates uninstalled the driver and broke everything again.

That was a few weeks ago. I'm confident now, a few updates later, that I'm using the correct driver and that settings are all good, so I'll document what it took. Some may be unnecessary steps but since I got it working once and haven't experimented further, I can't say.

* in BIOS settings, I had to enable `iGPU multi-monitor` and enable `CPUgraphics`

* install CUDA tools

  ```bash
  sudo apt install nvidia-cuda-toolkit
  ```

  

* install cudnn from NVIDIA; requires an account

* install a *headless* driver and accompanying utils

  ```bash
  sudo apt install nvidia-headless-440 nvidia-utils-440
  ```

  

* add to PATH and LD_LIBRARY_PATH in .bashrc

  ```bash
  export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}
  export LD_LIBRARY_PATH=/usr/local/cuda/lib64
  ```

  

* create a new config file in `/etc/X11/xorg.conf` with settings

  ```
  Section "ServerLayout"
      Identifier     "Layout0"
      Screen      0  "Screen0"
  EndSection
  
  Section "Screen"
      Identifier     "Screen0"
      Device         "intel"
  EndSection
  
  Section "Device"
      Identifier      "intel"
      Driver          "intel"
      VendorName      "Intel Corporation"
      BusId           "PCI:0:2:0"
      Option "AccelMethod" "sna"
      Option "TearFree" "true"
      Option "DRI" "3"
  EndSection
  ```

  

* modify grub settings in `/etc/default/grub` so that 

  ```
  GRUB_CMDLINE_LINUX="nogpumanager"
  ```

  then run `sudo update-grub` for the settings to take effect

* if, in the process, the file `/usr/share/X11/xorg.conf.d/11-nvidia-prime.conf` was created: delete it

* finally, last but not least, following random/good internet [advice](http://litaotju.github.io/2019/03/13/=Use-intel-for-display-nvidia-for-computing/), add (create?) the following to `/etc/modprobe.d/blacklist-nvidia.conf`

  ```
  blacklist nvidia-drm
  alias nvidia-drm off
  ```

  

Now all should be working. To be sure, running `nvidia-smi` should show something like  

```
Fri Sep 11 19:45:45 2020       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 450.66       Driver Version: 450.66       CUDA Version: 11.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  GeForce RTX 2070    Off  | 00000000:02:00.0 Off |                  N/A |
| 35%   47C    P0    22W / 175W |      0MiB /  7982MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```

And, in e.g. a jupyter notebook, running `tf.config.list_physical_devices('GPU')` should output the 

```
[PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]
```

Eureka! All the memory for ML!