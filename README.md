# Install Python on Windows

Or more precisely: Windows WSL Setup for Python Development

This is a quick reference to set up a Linux environment for Python development on Windows.
Used tools are WSL, Ubuntu, Pyenv, VSCode and GitHub.

### Table of Contents

[Installation Quick Guide](#installation-quick-guide)
1. [WSL](#1-wsl)
2. [Ubuntu](#2-ubuntu)
3. [Pyenv and Virtualenv](#3-pyenv-and-virtualenv)
4. [Python Build Dependencies](#4-python-built-dependencies)
5. [Install Python](#5-install-python)
6. [Virtual Environment](#6-virtual-environment)
7. [GitHub SSH Connection](#7-github-ssh-connection)
8. [VSCode](#8-vscode)

[Further Tips](#further-tips)

## Installation Quick Guide

The following notes are a quick reference.
If you run into issues, please follow the official documentations.

### 1. WSL

- Install WSL by following the [official Windows installation guide](https://learn.microsoft.com/en-us/windows/wsl/install)
- WSL 2 is what we want

### 2. Ubuntu

- Install Ubuntu via the Microsoft Store
- Choose the version you want or simply Ubuntu
- To start the console search for Ubuntu in the Windows Search
- On first start set your Ubuntu username and password

### 3. Pyenv and Virtualenv

- Pyenv and Virtualenv manage Python versions and virtual environments, respectively
- Install pyenv via

	```sh
	$ curl https://pyenv.run | bash
	```

- Run the following lines to add the configurations to your `~/.bashrc` file:

	```sh
	echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
	echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
	echo 'eval "$(pyenv init -)"' >> ~/.bashrc
	```

- Add the same lines to `~/.profile`:

	```sh
	echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
	echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
	echo 'eval "$(pyenv init -)"' >> ~/.profile
	```

- In order to automatically load the Virtualenv plugin run
	
	```sh
	$ echo eval "$(pyenv virtualenv-init -)" >> ~/.bashrc
	```

- Reboot shell via
	
	```sh
	$ source ~/.bashrc
	```

In case of issues: Official [pyenv Github repository](https://github.com/pyenv/pyenv) with installation instructions.

### 4. Python Built Dependencies

- To be able to install Python versions, run

	```sh
	sudo apt update; sudo apt install build-essential libssl-dev zlib1g-dev \
	libbz2-dev libreadline-dev libsqlite3-dev curl \
	libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
	```

### 5. Install Python

- List available Python versions:
	```sh
	$ pyenv install --list
	```

- Install a Python version:
	```sh
	$ pyenv install <python_version>
	```

- Use `$ pyenv --help` to see the available commands

### 6. Virtual Environment

- Create a venv:

	```sh
	$ pyenv virtualenv <installed_python_version> <venv_name>
	```

- Activate a venv:
	
	```sh
	$ pyenv activate <venv_name>
	```

- Overview of installed Python versions and related venvs:
	```sh
	$ pyenv versions
	```
	An asterisk will highlight the currently activated environment.

- Delete an environment via
	```sh
	$ pyenv virtualenv-delete <venv_name>
	```

### 7. GitHub SSH Connection

- The SSH setup allows us to omit the manual login process
- Create a GitHub account, if you don't have one yet
- Generate a new SSH key:

	```sh
	$ ssh-keygen -t ed25519 -C "your_email@example.com"
	```

	When prompted, press Enter to accept the default file location and name (else you will run into issues after every reboot)
- Start the ssh-agent:

	```sh
	$ eval "$(ssh-agent -s)"
	> Agent pid 59566
	```
	
- Add your private ssh key to the ssh-agent (the file without `.pub` ending)

	```sh
	ssh-add ~/.ssh/id_ed25519
	```

- Print your SSH public key via `$ cat id_rsa.pub` and copy it
- Visit the GitHub website and access your account settings (click your icon and choose **Settings**)
- Go to **SSH and GPG keys** and click **New SSH key**
- Give it a describing name, copy the key and save it

In case of issues: Official [GitHub SSH guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).

- To clone a repo copy its SSH link and use it via
    ```sh
    $ git clone <ssh_repo_link>
    ```

### 8. VSCode

- Install VSCode via Microsoft Store or the official [VSCode website](https://code.visualstudio.com/)
- To open the current directory in VSCode use
	
	```sh
	$ code .
	```

- Replace the dot with a path to open the respective directory in VSCode


## Further Tips

### File Access Across WSL and Windows

- Access Windows folders in WSL via the path `/mnt/c/`, e.g. `/mnt/c/Users/<user_name>/Downloads`

### Console Customization

- In Windows Search search for "terminal| or "Ubuntu"
- Right-click the top frame of the terminal and choose **Settings**
- Under Startup set your default profile to Ubuntu
- Go to **Profiles → Ubuntu → Appearance** to change color scheme, font and font size, etc.
- Customize further settings if interested, e.g. Appearance
