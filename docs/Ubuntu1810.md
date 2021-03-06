# 1. Ubuntu 18.04 for Azure Developers

[Ubuntu for Azure Developers](../README.md)

|Author|Dave Glover, Microsoft Australia|
|----|---|
|Platform| [Ubuntu 18.04 for Azure Developers](../docs/Ubuntu1804.md), [Kubuntu 18.04 for Azure Developers](../docs/Kubuntu1804.md), [Ubuntu 16.04 for Azure Developers](../docs/Ubuntu1604.md)|
|Date|As at May 2018|
|System| Lenovo ThinkPad X1 Carbon Gen 1|

<!-- TOC -->

- [1. Ubuntu 18.04 for Azure Developers](#1-ubuntu-1804-for-azure-developers)
    - [1.1. Installing the Essentials](#11-installing-the-essentials)
        - [1.1.1. Visual Studio Code](#111-visual-studio-code)
        - [1.1.2. Visual Studio Extensions](#112-visual-studio-extensions)
        - [1.1.3. GitHub Client](#113-github-client)
        - [1.1.4. Installing the latest .NET Core SDK](#114-installing-the-latest-net-core-sdk)
        - [1.1.5. Azure Storage Explorer](#115-azure-storage-explorer)
        - [1.1.6. Azure Storage Emulator](#116-azure-storage-emulator)
        - [1.1.7. Azure CLI (Command Line Interface)](#117-azure-cli-command-line-interface)
    - [1.2. Azure Functions with Visual Studio Code](#12-azure-functions-with-visual-studio-code)
        - [1.2.1. Install Azure Functions Core Tools](#121-install-azure-functions-core-tools)
    - [1.3. Toolkit](#13-toolkit)
        - [1.3.1. Docker](#131-docker)
        - [1.3.2. Installing Anaconda Distribution 5](#132-installing-anaconda-distribution-5)
        - [1.3.3. Tensorflow](#133-tensorflow)
            - [1.3.3.1. Python Support](#1331-python-support)
            - [1.3.3.2. Installing locally with nVidia GPU support](#1332-installing-locally-with-nvidia-gpu-support)
            - [1.3.3.3. NVIDIA Container Runtime for Docker](#1333-nvidia-container-runtime-for-docker)
        - [1.3.4. Microsoft Cognitive Toolkit](#134-microsoft-cognitive-toolkit)
            - [1.3.4.1. With nVidia CPU Support](#1341-with-nvidia-cpu-support)
        - [1.3.5. Postman](#135-postman)
        - [1.3.6. Fiddler](#136-fiddler)
        - [1.3.7. VirtualBox](#137-virtualbox)
    - [1.4. Internet of Things](#14-internet-of-things)
        - [1.4.1. Azure IoT Hub Explorer](#141-azure-iot-hub-explorer)
        - [1.4.2. Azure IoT Edge](#142-azure-iot-edge)
            - [1.4.2.1. Building ARM Docker Images from an x64 Ubuntu Host](#1421-building-arm-docker-images-from-an-x64-ubuntu-host)
    - [1.5. Microsoft SQL Server for Linux](#15-microsoft-sql-server-for-linux)
        - [1.5.1. Microsoft SQL Server for Linux (Dockerised)](#151-microsoft-sql-server-for-linux-dockerised)
        - [1.5.2. Microsoft SQL Server Operations Studio](#152-microsoft-sql-server-operations-studio)
        - [1.5.3. Microsoft SQL Server Extension for Visual Studio Code](#153-microsoft-sql-server-extension-for-visual-studio-code)
    - [1.6. Embedded Development](#16-embedded-development)
        - [1.6.1. Arduino](#161-arduino)
        - [1.6.2. Fritzing](#162-fritzing)
    - [1.7. Samples](#17-samples)
        - [1.7.1. Azure IoT Edge Samples](#171-azure-iot-edge-samples)
        - [1.7.2. Debugging .NET Core apps in Docker Containers from Visual Studio Code on Linux](#172-debugging-net-core-apps-in-docker-containers-from-visual-studio-code-on-linux)

<!-- /TOC -->



This guide assumes you have some experience with Linux and you will open Terminal and Ctrl-Shift-V to paste in [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) commands.

**Feel free to contribute to this guide.**

## 1.1. Installing the Essentials

### 1.1.1. Visual Studio Code

[Visual Studio Code](https://code.visualstudio.com/) is a must have IDE, open source, extensible, great language, debugging and tooling support.  

Head to [Visual Studio Code](https://code.visualstudio.com/) and download the .deb file for Debian and Ubuntu then install with QApt Package Installer.

### 1.1.2. Visual Studio Extensions

There are a stack of great extensions for Visual Studio Code. These are the ones that I find most useful.

1. Azure Account, Azure Functions, Azure CLI Tools, Azure Event Hub Explorer, Azure Cosmos DB, Azure IoT Edge, Azure IoT Toolkit, SQL Server, C#, Docker, Python, C/C++, JSON Tools, JSON Escaper, Powershell, Azure Application Insights, Azure App Services, Arduino, Azure Resource Manager Tools, Azure Storage, Tools for AI, Markdown TOC, Code Spell Checker, Docker, Docs Authoring Pack, and more...

### 1.1.3. GitHub Client

When you start Visual Studio Code for the first time you'll be prompted to install the GitHub client.

```bash
sudo apt install git
```

Before you can commit any changes against GitHub you'll need to configure who you are.

```bash
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

If you are using GitHub two-factor authentication then you'll need to create a GitHub token that you need to store securely. See [Creating a personal access token for the command line](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) for more information. You'll need to use this token in place of your password when pushing changes to GitHub.

Check out [Caching your GitHub password in Git](https://help.github.com/articles/caching-your-github-password-in-git/) to cache your GitHub credentials so you won't be asked for your credentials every time you push/sync you repository. 

In summary you need to run the following commands. Personally I use a much bigger number than 3600.

```bash
git config --global credential.helper 'cache --timeout=3600'
```

If you are using Visual Studio Team Services then checkout [Use Git Credential Managers to Authenticate to VSTS](https://docs.microsoft.com/en-gb/vsts/git/set-up-credential-managers?view=vsts)

### 1.1.4. Installing the latest .NET Core SDK

1. Install the latest release of the [.NET Core SDK]

```bash
sudo snap install dotnet-sdk && \
sudo snap alias dotnet-sdk.dotnet dotnet
```

2. Confirm successful installation of .NET Core SDK

```bash
dotnet --version
```

3. To refresh the installation on .NET Core

```bash
sudo snap refresh dotnet-sdk
```

[Set a Snap alias for dotnet](https://github.com/dotnet/core-setup/issues/4230)


### 1.1.5. Azure Storage Explorer

1. Install required dependency

```bash
sudo apt install libgconf-2-4 libcanberra-gtk0 libgnome-keyring0
```

2. Next [Download and Install Storage Explorer. Be sure to select Linux from the drop-down.](https://azure.microsoft.com/en-au/features/storage-explorer/)

5. The following Bash commands extract the Storage Explorer .tar.gz file to the /opt directory, and add a symbolic link to the StorageExplorer executable.

```bash
cd ~/Downloads && \
sudo mkdir -p /opt/StorageExplorer-linux-x64 && \
sudo tar -C $_ -zxvf StorageExplorer-linux-x64.tar.gz && \
sudo ln -s /opt/StorageExplorer-linux-x64/StorageExplorer /usr/bin/StorageExplorer

```

6. Create Storage Explorer [Ubunutu/KDE](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html) Desktop Resource

```bash
mkdir -p ~/.local/share/applications && \
cat > ~/.local/share/applications/StorageExplorer.desktop <<EOL
[Desktop Entry]
Encoding=UTF-8
Name=Storage Explorer
Exec=StorageExplorer
Icon=/opt/StorageExplorer-linux-x64/resources/app/out/app/icon.png
Terminal=false
Type=Application
Categories=Development;
EOL

```

Notes.
* [Microsoft Azure Storage Explorer release notes](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-relnotes)
* https://answers.launchpad.net/ubuntu/bionic/amd64/libcanberra-gtk0

### 1.1.6. Azure Storage Emulator

Install [Azurite](https://github.com/azure/azurite), a lightweight server clone of Azure Blob, Queue, and Table Storage that simulates most of the commands supported by it with minimal dependencies.

Notes.
* [Configure Azure Storage connection strings](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)
* [Connect to the emulator account using the well-known account name and key](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#connect-to-the-emulator-account-using-the-well-known-account-name-and-key)

### 1.1.7. Azure CLI (Command Line Interface)

Be sure that 'curl' is installed.

```bash
sudo apt install curl
```

[Install Azure CLI 2.0 with apt](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt?view=azure-cli-latest)

## 1.2. Azure Functions with Visual Studio Code

[Code and test Azure Functions locally](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local)

[Azure Functions Core Tools (note updated instructions for Ubuntu 18.04)](https://github.com/Azure/azure-functions-core-tools/blob/master/README.md)

### 1.2.1. Install Azure Functions Core Tools

As at August 2018 see [Install the Azure Functions Core Tools](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local#linux)

````bash
cd ~/Downloads && \
sudo apt install curl -y

curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg

sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-$(lsb_release -cs)-prod $(lsb_release -cs) main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-get update

sudo apt-get install azure-functions-core-tools

````

## 1.3. Toolkit

### 1.3.1. Docker

```bash
sudo apt update

sudo apt install -y apt-transport-https ca-certificates curl software-properties-common && \
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && \
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"

sudo apt update

sudo apt install -y docker-ce && \
sudo systemctl status docker
```

It's useful to add your user sudo rights to Docker. Note, you'll need to restart your system for this setting to take effect.

```bash
sudo usermod <Your User Name> -aG docker
```

Notes.

* [How to Install and Use Docker on Ubuntu 18.04 ](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04)

### 1.3.2. Installing Anaconda Distribution 5

It is a free, easy-to-install package manager, environment manager and Python distribution with a collection of 1,000+ open source packages with free community support. Anaconda is platform-agnostic, so you can use it whether you are on Windows, macOS or Linux.

[Installing Anaconda on Linux](https://docs.anaconda.com/anaconda/install/linux)

Create an Anaconda Navigator Desktop Resource

```bash
mkdir -p ~/.local/share/applications && \
cat > ~/.local/share/applications/anaconda-navigator.desktop <<EOL
[Desktop Entry]
Encoding=UTF-8
Name=Anaconda
Exec=/home/dave/anaconda3/bin/anaconda-navigator
Icon=/home/dave/anaconda3/lib/python3.6/site-packages/anaconda_navigator/static/images/anaconda-icon-256x256.png
Terminal=false
Type=Application
Categories=Development;
EOL
```

Notes.

1. [Anaconda Cheat Sheet](https://docs.anaconda.com/_downloads/Anaconda-Starter-Guide-Cheat-Sheet.pdf)
2. [How to check your Anaconda version and updating](https://medium.com/@mauridb/how-to-check-your-anaconda-version-c092400c9978)

### 1.3.3. Tensorflow

#### 1.3.3.1. Python Support

If you want Tensorflow with GPU support for use with Python then by far the easiest way to install is with Anaconda as it will install the complete CUDA toolkit and cuDNN library into your selected environment. But note, this is community supported, and not officially supported.

1. Create the Anaconda environment

    This would create a Anaconda environment with tensorflow-gpu support (requires an tensorflow capable nVida GPU, alternatively specify tersorflow-cpu), targeting Python 3.5, plus adds pylint useful in Visual Studio Code, and Jupyter Notebook support.

    ```bash
    conda create -n <envName> python=3.5 tensorflow-gpu pylint scipy jupyter requests scikit-learn
    ```

2. Activate the Anaconda environment

    Activate the Anaconda environment

    ```bash
    source activate <envName>
    ```

3. Deactivate an Anaconda Environment

    ```bash
    source deactivate
    ```

    Anaconda Navigator is the easiest way to manage Anaconda environments and launch environments.

    ```bash
    anaconda-navigator
    ```

4. Create your Python Project, open it with Visual Studio Code add a python file and select the Tensorflow environment you just created.

#### 1.3.3.2. Installing locally with nVidia GPU support

See 

1. [Installing Tensorflow GPU on Ubuntu 18.04 LTS](https://medium.com/@taylordenouden/installing-tensorflow-gpu-on-ubuntu-18-04-89a142325138)
2. [Installing Tensorlow, using pip in Anaconda](https://www.tensorflow.org/install/install_linux#InstallingAnaconda)


```bash
pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.10.1-cp35-cp35m-linux_x86_64.whl pylint scipy
```



#### 1.3.3.3. NVIDIA Container Runtime for Docker

If your PC has a nVidia GPU and you want to developer with  Docker and TensorFlow-GPU support. Simpler than installing CUDA Driver and Toolkit on to local system.

![](https://cloud.githubusercontent.com/assets/3028125/12213714/5b208976-b632-11e5-8406-38d379ec46aa.png)

Notes.

1. [Using TensorFlow via Docker](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/tools/docker/README.md)
2. [NVIDIA Container Runtime for Docker](https://github.com/NVIDIA/nvidia-docker)


### 1.3.4. Microsoft Cognitive Toolkit

For information on setting up [CNTK Docker Containers](https://docs.microsoft.com/en-us/cognitive-toolkit/CNTK-Docker-Containers).

#### 1.3.4.1. With nVidia CPU Support

1. Ensure the [NVIDIA Container Runtime for Docker](https://github.com/nvidia/nvidia-docker) is installed.

    ```bash
    nvidia-docker run -d -p 8888:8888 --name cntk-jupyter-notebooks -t microsoft/cntk
    ```

2. Start Jupyter Notebook server in your Docker container:

    ```bash
    docker exec -it cntk-jupyter-notebooks bash -c "source /cntk/activate-cntk && jupyter-notebook --no-browser --port=8888 --ip=0.0.0.0 --notebook-dir=/cntk/Tutorials --allow-root"
    ```

### 1.3.5. Postman

Install library dependency

```bash
sudo apt install libgconf-2-4
```

Download and Install Postman

```bash
cd ~/Downloads && \
wget https://dl.pstmn.io/download/latest/linux64 -O postman.tar.gz && \
sudo tar -xzf postman.tar.gz -C /opt && \
rm postman.tar.gz && \
sudo ln -s /opt/Postman/app/Postman /usr/bin/postman

```

Create Postman Desktop Resource

```bash
cat > ~/.local/share/applications/postman.desktop <<EOL
[Desktop Entry]
Encoding=UTF-8
Name=Postman
Exec=postman
Icon=/opt/Postman/app/resources/app/assets/icon.png
Terminal=false
Type=Application
Categories=Development;
EOL

```

Notes.

* Follow instruction at [How to Install the Postman Native App in Ubuntu 16.04](https://blog.bluematador.com/posts/postman-how-to-install-on-ubuntu-1604/)

### 1.3.6. Fiddler

See [Use Fiddler in Ubuntu](https://medium.com/@rajsek/use-fiddler-in-ubuntu-82b1dfd80848)

### 1.3.7. VirtualBox

```bash
sudo apt-get install virtualbox
```

## 1.4. Internet of Things

### 1.4.1. Azure IoT Hub Explorer

```bash
az extension add --name azure-cli-iot-ext
```

[az iot Command Guide](https://docs.microsoft.com/en-us/cli/azure/ext/azure-cli-iot-ext/iot?view=azure-cli-latest)

Example IoT Hub command

```bash
az iot hub monitor-events --hub-name IotHubName
```

Notes.

* [Installing and using iothub-explorer](https://github.com/Azure/iothub-explorer)
* [Microsoft Azure IoT Extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension/blob/master/README.md)


### 1.4.2. Azure IoT Edge

* [Develop and deploy a C# IoT Edge module to your simulated device - preview](https://docs.microsoft.com/en-us/azure/iot-edge/tutorial-csharp-module)

#### 1.4.2.1. Building ARM Docker Images from an x64 Ubuntu Host

If you are targeting ARM for your Docker builds then you will need to run the following command before you do your Docker build.

```bash
docker run --rm --privileged multiarch/qemu-user-static:register --reset
```

Notes.

* If your docker ARM base image is already built to include QEMU then register QEMU in the build agent as follows.
* Otherwise follow the instruction on [How to Build ARM Docker Images on Intel host](http://www.hotblackrobotics.com/en/blog/2018/01/22/docker-images-arm/)

## 1.5. Microsoft SQL Server for Linux

### 1.5.1. Microsoft SQL Server for Linux (Dockerised)

[Install SQL Server and create a database on Ubuntu](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-linux-2017)

Note, deleting a Microsoft SQL Server Docker container will also delete its data. So docker run to download and create and run the docker SQL Container and then use docker stop and start to control.

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
-p 1433:1433 --name sql1 \
-d microsoft/mssql-server-linux:2017-latest

```

To **stop** the Microsoft SQL Server Docker container.

```bash
docker stop sql1
```

To **start** the Microsoft SQL Server Docker container.

```bash
docker start sql1
```

Notes.

* [Run the SQL Server 2017 container image with Docker](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-linux-2017)

### 1.5.2. Microsoft SQL Server Operations Studio

Follow the notes for [Installing Microsoft SQL Operations Studio](https://docs.microsoft.com/en-gb/sql/sql-operations-studio/what-is?view=sql-server-linux-2017)

### 1.5.3. Microsoft SQL Server Extension for Visual Studio Code

[Use Visual Studio Code to create and run Transact-SQL scripts for SQL Server](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-develop-use-vscode?view=sql-server-linux-2017)

## 1.6. Embedded Development

### 1.6.1. Arduino

Download the [Arduino IDE](https://www.arduino.cc/en/Main/Software)

### 1.6.2. Fritzing

Download from [Fritzing Download Site](http://fritzing.org/download/).

I install in to a non system directory as Fritzing will complain that it doesn't have access rights to create parts bins.

```bash
cd ~/Downloads && \
mkdir -p ~/Apps && \
tar -C $_ -xvjf fritzing-0.9.3b.linux.AMD64.tar.bz2 && \
sudo ln -s ~/Apps/fritzing-0.9.3b.linux.AMD64/Fritzing /usr/bin/fritzing

```

Create Fritzing Desktop Resource file

```bash
cat > ~/.local/share/applications/fritzing.desktop <<EOL
[Desktop Entry]
Version=0.9.3b
Name=Fritzing
GenericName=Fritzing
Comment=Electronic Design Automation software
Exec=fritzing 
Icon=/home/dave/Apps/fritzing-0.9.3b.linux.AMD64/icons/fritzing_icon.png
Terminal=false
Type=Application
Categories=Development;IDE;Electronics;EDA;
X-SuSE-translate=false
StartupNotify=true
Categories=PCB;
MimeType=application/x-fritzing-fz;application/x-fritzing-fzz;application/x-fritzing-fzp;application/x-fritzing-fzpz;application/x-fritzing-fzb;application/x-fritzing-fzbz;application/x-fritzing-fzm;
EOL

```

## 1.7. Samples

### 1.7.1. Azure IoT Edge Samples

[Hands-on Grove Starter Kit for Azure IoT Edge](https://azure-samples.github.io/azure-iot-starter-kits/seeed/)

### 1.7.2. Debugging .NET Core apps in Docker Containers from Visual Studio Code on Linux

[This is a sample that demonstrates how to use vscode to build and debug dotnet core 2.0 console application in docker container](https://github.com/gloveboxes/docker.dotnet.debug)