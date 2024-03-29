# Guide for Lab502 Server with Xilinx Cards

English | [Chinese](./README_CN.md)

By Qianyu Cheng (qycheng@mail.ustc.edu.cn) 

**Note: Tutorial in Chinese is [here](./for_newbie.md)!!!**

## Feature Overview
- Security
  - Disable `sudo` for all users (except `ubuntu`)
  - ❌ Isolate bare-metal environment from clients by [`headnode`](./Dockerfile.headnode).
  - Allocate, execute and deallocate the environment in container mode (based on our scripts)
    ```bash
    env_alloc [-d <DeviceID[,...]>] [-s] [-p] [-i <Image>] [-v <Toolchain=20xx.x>] # allocate
    env_exec # execute
    env_dealloc # deallocate
    ```
  - Reserve data in `/data` directory of the container only (i.e. `/home/$USER` directory of host)
  - User creation script (`sudo` permission needed)
    ```bash
    /home/ubuntu/new_user_init.sh <username>
    ```
- Resource Management
  - Allocate FPGA cards (`-d DeviceID,...`)
  - Shared/exclusive allocation (with `-s` or without `-s`)
  - Release FPGA cards with timers (after 2 hours)
- Service
  - `Portainer` (Web-based container management) support (`https://<IP>:2000`)
  - Multi-version environment switched by `-v`
  - Create an extended environment by `Dockerfile` from `vitis:main` environment
    - [Template](./Dockerfile.template) 
  - `Jupyter Lab` (Python IDE) (`-p`) and `X11 Forwarding` (GUI) support
  - Automatic port forwarding in `<IP>:2001-2010`

![](./images/demo.png)
