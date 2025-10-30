# docker_lec_massif

Docker development container for MASSIF (Modeling And Simulation of fault Stability in subsurface fluid Injection at Faults) lectures.

## Prerequisites

### All Operating Systems

1. **Visual Studio Code**: Download and install from [code.visualstudio.com](https://code.visualstudio.com/)

2. **Docker Desktop**:
   - **Linux**: Install Docker Engine following the [official Docker documentation](https://docs.docker.com/engine/install/)
     - For Ubuntu/Debian: `sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`
     - Add your user to the docker group: `sudo usermod -aG docker $USER` (log out and back in for this to take effect)
   - **macOS**: Download and install [Docker Desktop for Mac](https://www.docker.com/products/docker-desktop/)
     - For Apple Silicon (M1/M2/M3): Use the Apple Chip version
     - For Intel processors: Use the Intel Chip version

3. **VS Code Extensions**:
   - **Dev Containers** (Required): Install from VS Code marketplace
     - Extension ID: `ms-vscode-remote.remote-containers`
     - This extension allows VS Code to work with Docker containers

### Windows Users Only (WSL2)

Windows users need to install Windows Subsystem for Linux 2 (WSL2):

1. **Install WSL2**:
   ```powershell
   wsl --install
   ```
   This will install Ubuntu by default. Restart your computer when prompted.

2. **Install Docker Desktop for Windows** from [docker.com](https://www.docker.com/products/docker-desktop/)
   - During installation, ensure "Use WSL 2 instead of Hyper-V" is selected
   - In Docker Desktop settings, go to Resources → WSL Integration and enable integration with your Ubuntu distribution

3. **Clone this repository inside WSL2**:
   - Open WSL2 terminal (Ubuntu)
   - Navigate to your desired directory
   - Clone the repository

## Installation Instructions

### Step 1: Clone the Repository

**Linux/macOS**:
```bash
git clone https://github.com/compgeo-mox/docker_lec_massif.git
cd docker_lec_massif
```

**Windows (in WSL2 terminal)**:
```bash
git clone https://github.com/compgeo-mox/docker_lec_massif.git
cd docker_lec_massif
```

### Step 2: Open in VS Code with Dev Container

1. **Launch VS Code**:
   - **Linux/macOS**: Open VS Code and use `File > Open Folder...` to open the `docker_lec_massif` directory
   - **Windows**: In WSL2 terminal, run `code .` from the `docker_lec_massif` directory

2. **Reopen in Container**:
   - VS Code should detect the `.devcontainer` folder and show a notification: *"Folder contains a Dev Container configuration file. Reopen folder to develop in a container"*
   - Click **"Reopen in Container"**
   
   Alternatively, use the Command Palette:
   - Press `F1` or `Ctrl+Shift+P` (Windows/Linux) / `Cmd+Shift+P` (macOS)
   - Type and select: **"Dev Containers: Reopen in Container"**

3. **Wait for Container Build**:
   - The first time, Docker will build the container (this may take 10-15 minutes)
   - VS Code will show the build progress in the terminal
   - Subsequent launches will be much faster

### Step 3: Verify Installation

Once the container is running:

1. Open a new terminal in VS Code (`Terminal > New Terminal`)
2. Verify Python installation:
   ```bash
   python --version
   ```
   Should show Python 3.13

3. Verify the lec_massif package:
   ```bash
   python -c "import lec_massif; print('lec_massif installed successfully')"
   ```

## Container Configuration

The development container includes:

- **Base Image**: Ubuntu (latest) on linux/amd64 platform
- **Python**: Version 3.13 via Miniconda
- **Jupyter**: Jupyter Notebook server (accessible on port 8888)
- **VS Code Extensions**:
  - Python support (ms-python.python)
  - Pylance language server
  - Black formatter
  - Flake8 linter
  - isort import organizer
  - Jupyter notebook support
  - Ruff formatter and linter
- **Additional Tools**: Git, build tools, LaTeX support for mathematical typesetting

## Using Jupyter Notebooks

The container exposes port 8888 for Jupyter:

1. In the VS Code terminal, start Jupyter:
   ```bash
   jupyter notebook --ip=0.0.0.0 --no-browser
   ```

2. Copy the URL with the token from the terminal output

3. Access it in your browser or use VS Code's built-in Jupyter support

## Working with the lec_massif Package

The container automatically clones and installs the `lec_massif` package in development mode. The package is located at `/home/user/lec_massif` inside the container.

## Troubleshooting

### Container fails to build
- Ensure Docker Desktop is running
- Check that you have sufficient disk space (at least 5GB free)
- Try rebuilding: `F1` → "Dev Containers: Rebuild Container"

### Permission issues (Linux)
- Ensure your user is in the docker group: `groups | grep docker`
- If not, run: `sudo usermod -aG docker $USER` and log out/in

### Port 8888 already in use
- Stop other Jupyter instances or change the port in `.devcontainer/devcontainer.json`

### macOS Performance (Apple Silicon)
- The container uses `linux/amd64` platform and runs through Rosetta 2 emulation
- Performance should be acceptable but may be slower than native ARM64 images

## Repository Structure

```
docker_lec_massif/
├── .devcontainer/
│   ├── devcontainer.json    # VS Code Dev Container configuration
│   └── Dockerfile            # Docker image definition
├── LICENSE
└── README.md
```

## Contributing

Feel free to open issues or submit pull requests to improve the development environment.

## License

See the [LICENSE](LICENSE) file for details.