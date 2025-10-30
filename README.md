# MASSIF Docker Development Environment

> **Dockerized Development Environment for Modeling and Simulation of Fault Stability in Subsurface Fluid Injection**

This repository provides a ready-to-use Docker development container for the [lec_massif](https://github.com/compgeo-mox/lec_massif) course. The container includes all necessary dependencies, tools, and pre-configured VS Code extensions to work with the computational laboratories on fault mechanics and subsurface fluid flow.

## About the Course

This course introduces mathematical and numerical modeling of fault stability in subsurface settings influenced by fluid injection and production. The computational laboratories cover:

- **Darcy's Equation**: Flow in porous media with finite element/volume discretizations
- **Linear Elasticity**: Stress and displacement field analysis in rocks
- **Biot's Poroelastic Equations**: Coupled hydro-mechanical problems
- **Decoupling Strategies**: Fixed-strain and fixed-stress methods for poroelasticity
- **Contact Mechanics**: Fault slip criteria and Coulomb failure analysis
- **Fault Stability Assessment**: Methods for evaluating fault activation risk

The laboratories are implemented as Jupyter notebooks using modern Python scientific computing libraries, including [PorePy](https://github.com/pmgbergen/porepy) and [PyGeoN](https://github.com/compgeo-mox/pygeon).

## Why Use This Docker Container?

This Docker environment eliminates installation complexity and ensures reproducibility by providing:

✅ **Pre-configured Python 3.13 environment** with Miniconda  
✅ **Automatic installation** of the lec_massif package and all dependencies  
✅ **Jupyter Notebook support** for interactive computing  
✅ **VS Code integration** with Python, Jupyter, and formatting extensions  
✅ **LaTeX support** for mathematical typesetting  
✅ **Cross-platform compatibility** (Linux, macOS, Windows via WSL2)  
✅ **Consistent development environment** across all machines  

No more "it works on my machine" problems!

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

### Running the Laboratory Notebooks

1. Navigate to the lab directory:
   ```bash
   cd /home/user/lec_massif/lab
   ```

2. Open any lab notebook in VS Code (e.g., `lab1/ex1.ipynb`)

3. VS Code will automatically detect the Jupyter kernel and allow you to run cells interactively

4. Follow the instructions in each notebook and run cells sequentially

### Visualizing Results

Many labs export results as `.vtu` files for visualization:

- Files are typically saved in the working directory
- Use [ParaView](https://www.paraview.org/) to open and visualize `.vtu` files
- ParaView can be installed on your host machine (not in the container)

### Key Dependencies

The environment includes:

- **PorePy**: Framework for simulation of flow and transport in fractured and porous media
- **PyGeoN**: Geometric tools and discretization methods for subsurface modeling
- **NumPy/SciPy**: Numerical computing and linear algebra
- **Matplotlib**: Plotting and visualization
- **Jupyter**: Interactive notebooks

## Learning Outcomes

By completing the laboratories in this environment, you will:

- Understand mathematical formulations of Darcy's equation, linear elasticity, and Biot's poroelastic equations
- Discretize and solve PDEs using finite element and finite volume methods
- Analyze coupled hydro-mechanical effects on fault stress changes
- Apply contact mechanics and fault slip criteria (Coulomb failure)
- Assess stability for fault activation in fluid injection scenarios
- Develop practical skills in scientific computing with Python
- Master debugging, validation, and visualization techniques

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

## Related Resources

- **Main Course Repository**: [compgeo-mox/lec_massif](https://github.com/compgeo-mox/lec_massif)
- **PorePy Documentation**: [github.com/pmgbergen/porepy](https://github.com/pmgbergen/porepy)
- **PyGeoN Documentation**: [github.com/compgeo-mox/pygeon](https://github.com/compgeo-mox/pygeon)
- **ParaView**: [www.paraview.org](https://www.paraview.org/)

## Support

For issues related to:
- **Docker container setup**: Open an issue in this repository
- **Course content and laboratories**: Open an issue in [lec_massif](https://github.com/compgeo-mox/lec_massif/issues)
- **VS Code Dev Containers**: Consult the [official documentation](https://code.visualstudio.com/docs/devcontainers/containers)

## Contributing

Improvements to the Docker environment are welcome! Feel free to:
- Report bugs or issues
- Suggest enhancements
- Submit pull requests

## License

This project is licensed under the GPL-3.0 License - see the [LICENSE](LICENSE) file for details.

The [lec_massif](https://github.com/compgeo-mox/lec_massif) course materials are also licensed under GPL-3.0.