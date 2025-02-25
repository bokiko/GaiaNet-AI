# Gaia Node: Quick Installation Guide

## What is Gaia Node?
Gaia Node is an open-source platform for building, launching, and monetizing AI agents. By running a node, you join a decentralized AI network and earn rewards by sharing your computing power.

## System Requirements
- **Operating System:** Ubuntu 20.04/22.04 (WSL on Windows supported)
- **GPU (Recommended):**
  - **8GB VRAM:** RTX 3060 Ti, RTX 3070, RTX 4060, RTX 4060 Ti, A10G
  - **10-12GB VRAM:** RTX 3080, RTX 3080 Ti, RTX 4070, RTX 4070 Ti, A10, A2000
  - **16-24GB VRAM:** RTX 3090, RTX 3090 Ti, RTX 4080, RTX 4090, A4000, A5000, A6000, A100 (24GB)
  - **32-80GB VRAM:** A100 (40GB/80GB), A30, A40, H100
- **CPU (for non-GPU setup):** Any modern CPU (Apple Silicon M1-M4 supported)
- **RAM:** 16GB+ recommended (8GB minimum)

## Preparation

Connect to your machine via SSH using Termius and follow these steps:

### 1. Update Your System
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y nano curl wget lsof build-essential libgomp1
```

### 2. Install/Update NVIDIA Drivers
For NVIDIA GPU systems, install the latest drivers:
```bash
sudo ubuntu-drivers autoinstall
sudo reboot
```

After reboot, reconnect via SSH and verify your GPU is detected:
```bash
nvidia-smi
```

You should see your GPU listed with driver information.

## Installation

```bash
curl -sSfL 'https://github.com/GaiaNet-AI/gaianet-node/releases/latest/download/install.sh' | bash
```

After installation completes, load the environment variables:

```bash
source ~/.bashrc
```

## Configure and Start Your Node

1. Initialize the node with a model appropriate for your GPU:

   **For 8GB VRAM GPUs (RTX 3060 Ti, 3070, RTX 4060, 4060 Ti, A10G):**
   ```bash
   gaianet init --config https://raw.githubusercontent.com/GaiaNet-AI/node-configs/main/qwen-1.5-0.5b-chat/config.json
   ```

   **For 10-12GB VRAM GPUs (RTX 3080, 3080 Ti, RTX 4070, 4070 Ti, A10, A2000):**
   ```bash
   gaianet config --chat-url https://huggingface.co/gaianet/Llama-3.2-3B-Instruct-GGUF/resolve/main/Meta-Llama-3.2-3B-Instruct-Q5_K_M.gguf --chat-ctx-size 4096 --prompt-template llama-3-chat
   gaianet init
   ```
   
   **For 32-80GB VRAM GPUs (A100, A30, A40, H100):**
   ```bash
   gaianet config --chat-url https://huggingface.co/gaianet/Llama-3-70B-Instruct-GGUF/resolve/main/Llama-3-70B-Instruct-Q4_K_M.gguf --chat-ctx-size 32768 --prompt-template llama-3-chat
   gaianet init
   ```

   **For 16-24GB VRAM GPUs (RTX 3090, 3090 Ti, RTX 4080, 4090, A4000, A5000, A6000):**
   ```bash
   gaianet config --chat-url https://huggingface.co/gaianet/Qwen1.5-7B-Chat-Q5_K_M/resolve/main/Qwen1.5-7B-Chat-Q5_K_M.gguf --chat-ctx-size 32768 --prompt-template qwen-chat
   gaianet init
   ```

2. Start your node:
   ```bash
   gaianet start
   ```

3. Get your node information:
   ```bash
   gaianet info
   ```
   **Important:** Write down your Node ID and Device ID for registration.

## Register Your Node and Start Earning

1. Go to [https://gaianet.ai/reward](https://gaianet.ai/reward?invite_code=RXDpgT)
2. Connect your EVM wallet
3. Click "Node" → "CONNECT NODE"(you can use my code when asked for referral : RXDpgT)
4. Input your Node ID and Device ID from `gaianet info`
5. Click "Join Domain" and select "Rivalz"

You're now running a Gaia Node! Check your node points at [https://www.gaianet.ai/reward-summary](https://www.gaianet.ai/reward-summary)

## Troubleshooting

If you encounter errors during installation:

### "Too many open files" on macOS
```bash
ulimit -n 10000
```

### "libgomp.so.1: cannot open shared object file"
```bash
sudo apt update
sudo apt install -y libgomp1
```

### Port 8080 already in use
```bash
gaianet stop
gaianet config --port 8081
gaianet init
gaianet start
```

### CUDA installation issues
If you have Python-installed CUDA, create symbolic links:
```bash
ln -s /usr/local/lib/python3.10/dist-packages/nvidia/cublas/lib/libcublas.so.12 /usr/lib/libcublas.so.12
ln -s /usr/local/lib/python3.10/dist-packages/nvidia/cuda_runtime/lib/libcudart.so.12 /usr/lib/libcudart.so.12
ln -s /usr/local/lib/python3.10/dist-packages/nvidia/cublas/lib/libcublasLt.so.12 /usr/lib/libcublasLt.so.12
```

### Node Management Commands

To stop your node:
```bash
gaianet stop
```

To check node status:
```bash
gaianet info
```

To view node logs:
```bash
ls -la ~/gaianet/log/
```

To update your node to the latest version:
```bash
curl -sSfL 'https://github.com/GaiaNet-AI/gaianet-node/releases/latest/download/install.sh' | bash -s -- --upgrade
```
