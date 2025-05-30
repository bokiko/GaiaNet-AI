# Gaia Node: Complete Installation Guide

<div align="center">
  
![Gaia Node](https://storage.googleapis.com/gaianet-public/assets/website-media/gaia-logo-primary.png)

*Set up your Gaia Node and earn rewards by sharing computing power*

</div>

## What is Gaia Node?

Gaia Node is an open-source platform that enables you to:
- Build, launch, and monetize AI agents
- Join a decentralized AI network
- Earn rewards for sharing your computing power
- Run your own custom AI services

By running a Gaia Node, you're contributing to a distributed network of AI services while earning cryptocurrency rewards.

## System Requirements

### Hardware Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| **CPU** | Any modern CPU with 2+ cores | 4+ cores |
| **RAM** | 8GB | 16GB+ |
| **Storage** | 10GB free space | 20GB+ SSD |
| **GPU** | See VRAM table below | See VRAM table below |

### Hardware Requirements

Choose a model based on your hardware capabilities:

| Hardware | Supported Models | Recommended AI Model |
|----------|------------------|----------------------|
| **CPU or <8GB VRAM** | Any CPU, Integrated GPUs, Low-end GPUs | Qwen2-0.5B |
| **8GB VRAM** | RTX 3060 Ti, RTX 3070, RTX 4060, RTX 4060 Ti, A10G | Qwen1.5-0.5B |
| **10-12GB VRAM** | RTX 3080, RTX 3080 Ti, RTX 4070, RTX 4070 Ti, A10, A2000 | Llama-3.2-3B |
| **16-24GB VRAM** | RTX 3090, RTX 3090 Ti, RTX 4080, RTX 4090, A4000, A5000, A6000, A100 (24GB) | Qwen1.5-7B |
| **32-80GB VRAM** | A100 (40GB/80GB), A30, A40, H100 | Llama-3-70B |

### Supported Operating Systems

- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- macOS (for Apple Silicon M1-M4)
- Windows 11 (via WSL2)

## Pre-Installation Setup

### 1. System Updates and Dependencies

Connect to your machine via SSH using Termius or your preferred SSH client:

```bash
# Update system packages
sudo apt update && sudo apt upgrade -y

# Install required dependencies
sudo apt install -y nano curl wget lsof build-essential libgomp1
```

### 2. NVIDIA GPU Setup (Skip for non-NVIDIA systems)

Install and update NVIDIA drivers:

```bash
# Install latest recommended drivers
sudo ubuntu-drivers autoinstall

# Reboot to apply changes
sudo reboot
```

After rebooting, reconnect via SSH and verify GPU detection:

```bash
# Check if GPU is properly detected
nvidia-smi
```

You should see output showing your GPU model, driver version, and CUDA version.

## Gaia Node Installation

### 1. Install Gaia Node Software

Run the installation script:

```bash
curl -sSfL 'https://github.com/GaiaNet-AI/gaianet-node/releases/latest/download/install.sh' | bash
```

Set up environment variables:

```bash
source ~/.bashrc
```

### 2. Configure AI Model Based on Your Hardware

Select a configuration based on your hardware capabilities:

<details>
<summary><b>For CPU or GPUs with below 8GB VRAM</b></summary>

```bash
# Stop any running instance
gaianet stop

# Initialize with Qwen2-0.5B (optimized for CPU and low VRAM)
gaianet init --config https://raw.githubusercontent.com/GaiaNet-AI/node-configs/main/qwen2-0.5b-instruct/config.json

# Start the node
gaianet start
```
</details>

<details>
<summary><b>For 8GB VRAM GPUs (RTX 3060 Ti, 3070, 4060, 4060 Ti, A10G)</b></summary>

```bash
gaianet config --chat-url https://huggingface.co/gaianet/Qwen1.5-0.5B-Chat-GGUF/resolve/main/Qwen1.5-0.5B-Chat-Q5_K_M.gguf --chat-ctx-size 4096 --prompt-template qwen-chat
```

Alternative lightweight models for 8GB VRAM:

```bash
# Phi-3 Mini (better for some use cases)
gaianet config --chat-url https://huggingface.co/gaianet/Phi-3-mini-4k-GGUF/resolve/main/Phi-3-mini-4k-instruct-Q5_K_M.gguf --chat-ctx-size 4096 --prompt-template phi-chat

# Gemma 2B (balanced option)
gaianet config --chat-url https://huggingface.co/gaianet/gemma-2b-it-GGUF/resolve/main/gemma-2b-it-Q5_K_M.gguf --chat-ctx-size 4096 --prompt-template gemma-chat
```
</details>

<details>
<summary><b>For 10-12GB VRAM GPUs (RTX 3080, 3080 Ti, 4070, 4070 Ti, A10, A2000)</b></summary>

```bash
gaianet config --chat-url https://huggingface.co/gaianet/Llama-3.2-3B-Instruct-GGUF/resolve/main/Meta-Llama-3.2-3B-Instruct-Q5_K_M.gguf --chat-ctx-size 4096 --prompt-template llama-3-chat
```
</details>

<details>
<summary><b>For 16-24GB VRAM GPUs (RTX 3090, 3090 Ti, 4080, 4090, A4000-A6000)</b></summary>

```bash
gaianet config --chat-url https://huggingface.co/gaianet/Qwen1.5-7B-Chat-Q5_K_M/resolve/main/Qwen1.5-7B-Chat-Q5_K_M.gguf --chat-ctx-size 32768 --prompt-template qwen-chat
```
</details>

<details>
<summary><b>For 32-80GB VRAM GPUs (A100, A30, A40, H100)</b></summary>

```bash
gaianet config --chat-url https://huggingface.co/gaianet/Llama-3-70B-Instruct-GGUF/resolve/main/Llama-3-70B-Instruct-Q4_K_M.gguf --chat-ctx-size 32768 --prompt-template llama-3-chat
```
</details>

### 3. Initialize the Node

After configuring your model, initialize the node:

```bash
gaianet init
```

This process will:
- Download the selected AI model
- Set up the vector database
- Prepare the node dashboard
- Configure network connectivity

### 4. Start Your Node

Launch your node:

```bash
gaianet start
```

### 5. Get Node Information

Retrieve your node's unique identifiers:

```bash
gaianet info
```

**⚠️ Important:** Copy and save your Node ID and Device ID - you'll need these for registration.

## Register Your Node and Earn Rewards

1. Visit [Gaia Network Rewards](https://gaianet.ai/reward?invite_code=RXDpgT)
2. Connect your Ethereum-compatible wallet (Metamask, etc.)
3. Click "Node" → "CONNECT NODE"
4. Enter your Node ID and Device ID
5. When prompted for a referral code, enter: `RXDpgT`
6. Click "Join Domain" and select "Rivalz"

Congratulations! Your Gaia Node is now running and earning rewards. Monitor your node's performance and rewards at [Reward Summary](https://www.gaianet.ai/reward-summary).

## Advanced Configuration

### Customizing System Prompt

To change how your AI responds to queries:

```bash
gaianet config --system-prompt "You are a helpful AI assistant. Provide clear and accurate information to questions."
gaianet init
gaianet start
```

### Changing Default Port

If port 8080 is already in use:

```bash
gaianet stop
gaianet config --port 8081
gaianet init
gaianet start
```

## Auto-restart After Reboot

By default, your Gaia Node won't automatically restart after a system reboot. To set up auto-restart:

```bash
# Create a systemd service file
cat > /etc/systemd/system/gaianode.service << 'EOF'
[Unit]
Description=Gaia Node Service
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/root
ExecStart=/bin/bash -c "source /root/.bashrc && gaianet start"
Restart=on-failure
RestartSec=5s

[Install]
WantedBy=multi-user.target
EOF

# Enable and start the service
systemctl daemon-reload
systemctl enable gaianode.service
systemctl start gaianode.service
```

To check service status:
```bash
systemctl status gaianode.service
```

<details>
<summary><b>"Too many open files" error on macOS</b></summary>

Increase file descriptor limit:
```bash
ulimit -n 10000
```
Then restart your node in the same terminal session.
</details>

<details>
<summary><b>"libgomp.so.1: cannot open shared object file"</b></summary>

Install the missing library:
```bash
sudo apt update
sudo apt install -y libgomp1
```
</details>

<details>
<summary><b>CUDA installation issues</b></summary>

If you have Python-installed CUDA, create symbolic links:
```bash
ln -s /usr/local/lib/python3.10/dist-packages/nvidia/cublas/lib/libcublas.so.12 /usr/lib/libcublas.so.12
ln -s /usr/local/lib/python3.10/dist-packages/nvidia/cuda_runtime/lib/libcudart.so.12 /usr/lib/libcudart.so.12
ln -s /usr/local/lib/python3.10/dist-packages/nvidia/cublas/lib/libcublasLt.so.12 /usr/lib/libcublasLt.so.12
```
</details>

<details>
<summary><b>Node fails to start or crashes</b></summary>

Check the logs:
```bash
cat ~/gaianet/log/rag-api.log
cat ~/gaianet/log/qdrant.log
```

Try reinstalling with:
```bash
gaianet stop
curl -sSfL 'https://github.com/GaiaNet-AI/gaianet-node/releases/latest/download/install.sh' | bash -s -- --reinstall
source ~/.bashrc
```
Then reconfigure and restart.
</details>

## Node Management Commands

| Command | Description |
|---------|-------------|
| `gaianet stop` | Stop your node |
| `gaianet info` | Display node information |
| `gaianet config` | View or modify configuration |
| `ls -la ~/gaianet/log/` | View log files |
| `curl -sSfL 'https://github.com/GaiaNet-AI/gaianet-node/releases/latest/download/install.sh' \| bash -s -- --upgrade` | Update to latest version |

## Support and Community

For additional help, join our community:
- [Discord](https://discord.gg/gaianet)
- [Twitter/X](https://twitter.com/Gaianet_AI)
- [GitHub](https://github.com/GaiaNet-AI)

---

<div align="center">
  
*Created by Bokiko - Last updated February 2025*

</div>
