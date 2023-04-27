# Stable Diffusion: macOS install help

<p><img src="https://images.squarespace-cdn.com/content/v1/6213c340453c3f502425776e/0715034d-4044-4c55-9131-e4bfd6dd20ca/2_4x.png?format=960w"></p>

Stable Diffusion macOS install help is our guide for this kind of setup:

* [Stable Diffusion](https://stability.ai/blog/stable-diffusion-public-release) image generator
  
* [Apple macOS Monterey](https://www.apple.com/macos/monterey/) operating system, current version

* [MacBook Pro with M1 ARM chip and 32GB free RAM](https://www.apple.com/macbook-pro/), not x86-64 Intel chip, not less than 32GB free RAM

* [Homebrew](https://brew.sh) package manager

* [Python](https://www.python.org) programming language
 
* [cmake](https://cmake.org) build automation
  
* [git](https://www.git-scm.com) source code manager

* [protobuf](https://developers.google.com/protocol-buffers) data structures
 
* [Anaconda](https://www.anaconda.com) data science platform

See our Stable Diffusion image gallery:

➤ https://github.com/joelparkerhenderson/stable-diffusion-image-gallery



## Guide Goals

This guide is our notes about our preferred way of installing Stable Diffusion.

* If you want an easy way to try Stable Diffusion on macOS, then try this first: https://diffusionbee.com/

* If you want an easy way to try Stable Diffusion on macOS and other operating systems, then try this first: https://github.com/invoke-ai/InvokeAI

* If you want maximum configurability on macOS, and you willing to install a bunch of software pieces, then try this guide.

This guide is intentionally step-by-step, because we want to help more people be successful, including people who are trying these kinds of software installs for the first time.

* This guide is intentionally using steps that help multiple macOS users on the same system, because we want this guide to be able to help people who share a computer, such as teachers and students in schools.
  
* This guide is intentionally doing a "kitchen sink" approach of installing everything, because this can help our people with more capabilities as they try Stable Diffusion.

We welcome constructive feedback via GitHub issues, or pull requests, or email to joel@joelparkerhenderson.com.


## Thanks

Thanks to many developers working on Stable Diffusion and help for it, and special thanks to:

➤ https://www.assemblyai.com/blog/how-to-run-stable-diffusion-locally-to-generate-images/

➤ https://github.com/lstein/stable-diffusion/blob/main/README-Mac-MPS.md

➤ https://news.ycombinator.com/item?id=32678664


## Homebrew

Install:

```sh
% /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Verify the path is typical:

```sh
% brew --prefix
/opt/homebrew
```

Verify your system can locate the program:

```sh
% which brew
/opt/homebrew/bin/brew
```

Verify the version is 3.5.10 or higher:

```sh
% brew --version
Homebrew 3.5.10
```

Do any brew upgrades:

```sh
% brew upgrade
% brew upgrade --cask --greedy
```

Verify brew is working:

```sh
% brew doctor
```


## Python

Install:

```sh
brew install python
```

Verify the path is typical:

```sh
% brew --prefix python
/opt/homebrew/opt/python@3.11
```

Verify your system can locate the program:

```sh
% which python3
/opt/homebrew/bin/python3
```

Verify the version is 3.11 or higher:

```sh
% python3 --version
Python 3.11.3
```


## cmake

Install:

```sh
% brew install cmake
```

Verify the path is typical:

```sh
% brew --prefix cmake 
/opt/homebrew/opt/cmake
```

Verify your system can locate the program:

```sh
% which cmake
/opt/homebrew/bin/cmake
```

Verify the version is 3.26 or higher:

```sh
% cmake --version
cmake version 3.26.3
```


## git

Install:

```sh
% brew install git
```

Verify the path is typical:

```sh
% brew --prefix git  
/opt/homebrew/opt/git
```

Verify your system can locate the program:

```sh
% which git
/opt/homebrew/bin/git
```

Verify the version is 2.40 or higher:

```sh
% git --version
git version 2.40.0
```


## protobuf

Install:

```sh
% brew install protobuf
```

Verify the path is typical:

```sh
% brew --prefix protobuf
/opt/homebrew/opt/protobuf
```


## Anaconda

Install:

```sh
% brew install anaconda
```

Verify the version is 2023.03 or higher, and verify that the auto-update version is identical to the Caskroom version:

```sh
% brew info --cask anaconda
==> anaconda: 2023.03 (auto_updates)
…
/opt/homebrew/Caskroom/anaconda/2023.03 (304.8MB)
…
```

If the version is not 2023.03 or higher, or the auto-update version is not identical to the Caskroom version, then reinstall and reverify:

```sh
% brew reinstall --cask anaconda
…
==> Uninstalling Cask anaconda
…
==> Installing Cask anaconda
…
🍺  anaconda was successfully installed!

% brew info --cask anaconda
```


### Create /opt directory

We like to install software such as anaconda within a system-wide top-level directory named "/opt", rather than within your personal user directory named "/Users/me" or similar. 

This is because:

* The directory "/opt" is what brew does by default

* The "/opt" convention tends help with tutorials and troubleshooting as needed.

* The system-wide directory makes it easier for multiple system users to all use the same Anaconda installation; for us, this tends to helps teachers and students who need to use shared systems.

Ensure the system-wide top-level directory exists:

```sh
% mkdir -p /opt
```

In the next step, we will install anaconda to this directory:

```
/opt/anaconda3
```


### Script

Anaconda uses an installation shell script that you must run.

Find the script:

```sh
% find /opt/homebrew/Caskroom/anaconda -name "*.sh" 
```

Output shows the shell script name, which may use different version numbers depending on when you install Anaconda:

```sh
/opt/homebrew/Caskroom/anaconda/2023.03/Anaconda3-2023.03-MacOSX-arm64.sh
```

Run the shell script via `sudo` and `sh` and the script name from above:

```sh
% sudo sh /opt/homebrew/Caskroom/anaconda/2023.03/Anaconda3-2023.03-MacOSX-arm64.sh
```

Your system should prompt you to type your password, then should run the shell script.


### License

Anaconda prompts you to agree to the license:

```txt
Do you accept the license terms? [yes|no]
```

Type `yes`, then return.


### Directory

Anaconda prompts you to choose an installation directory:

```
Anaconda3 will now be installed into this location:
/Users/…/anaconda3

  - Press ENTER to confirm the location
  - Press CTRL-C to abort the installation
  - Or specify a different location below
```

If you are generally a novice user, then use the Anaconda default directory, such as:

```sh
/Users/me/anaconda3
```

If you are generally an advanced user, then you may want to use our preferred naming convention, which installs many programs into the user's `opt` directory, such as:

```sh
/Users/me/opt/anaconda3
```

Type your installation directory, then return.


### conda init

Anaconda prompts you to run this:

```txt
Do you wish the installer to initialize Anaconda3
by running conda init? [yes|no]
```

Type `yes`, then return.


### Success

Anaconda installs and advises you:

```txt
For changes to take effect, close and re-open your current shell.
```

Close your current shell. 

Open a new shell.

Verify the installation works by running Anaconda using its full path:

```sh
% /opt/anaconda3/condabin/conda --version
conda 23.1.0
```


### Path


Export your preferred path such as:

```sh
export PATH="$PATH:/opt/anaconda3/condabin"
```

Optionally, you can append the Anaconda path to your environment, such as by editing whichever of these files you use, then closing your shell and opening a new shell:

* `/etc/bashrc` 

* `/etc/zshrc`

* `$HOME/.bashrc` 

* `$HOME/.zshrc`

Verify there is exactly one `conda` program on your path:

```sh
% which conda
/opt/anaconda3/condabin/conda
```

If you have more than one `conda` program on your path, then you'll need to be sure you're doing the rest of this guide using `conda` that you want. 

  * You can adjust your path, so it chooses the right `conda` program first.
  
  * You can run conda via the full path `/opt/anaconda3/condabin/conda`.

  * You can uninstall the other `conda` programs, if no one on your system needs them.
  
Verify the version is 23.1.0 or higher:

```sh
% conda --version
conda 23.1.0
```


### Update

Update conda just in case it's changed recently:

```sh
% sudo conda update -n base -c defaults conda
```


## Stable Diffusion weights file

Download the Stable Diffusion weights file; heads up that the file is somewhat large, more than 4GB.


### Stable Diffusion verison 2

Download the Stable Diffision version 2 checkpoint file:

```sh
curl -O -L https://huggingface.co/stabilityai/stable-diffusion-2-base/resolve/main/512-base-ema.ckpt
```

We prefer to move the file into its own directory because that makes it easier to use among all the system users:

```sh
% sudo mkdir -p /opt/stable-diffusion-checkpoints/2.0/
% sudo mv 512-base-ema.ckpt /opt/stable-diffusion-checkpoints/2.0/
```


### Stable Diffision version 1 - DEPRECATED

Download the Stable Diffision version 1 checkpoint weights file:

```sh
curl -L https://huggingface.co/CompVis/stable-diffusion-v-1-4-original/resolve/main/sd-v1-4.ckpt > sd-v1-4.ckpt
```

We prefer to put the file in its own directory so it's easier to access for all our macOS users:

```sh
% sudo mkdir -p /opt/stable-diffusion-checkpoints/1.4/
% sudo mv sd-v1-4.ckpt /opt/stable-diffusion-checkpoints/1.4/
```


## Stable Diffusion repository

This section comes from:

➤ https://github.com/lstein/stable-diffusion/blob/main/README-Mac-MPS.md


### Install

Install:

```sh
% cd ~
% git clone https://github.com/lstein/stable-diffusion.git
% cd stable-diffusion
```

If you have previously installed the repository, then change into its directory, and reset the branch:

```sh
% git reset --hard origin/master.
```

### Link

Link to the CKPT file:

```sh
% mkdir -p models/ldm/stable-diffusion-v1/
% PATH_TO_CKPT="/opt/stable-diffusion-ckpt"  # use your own directory that contains your CPKT file
% ln -sfn "$PATH_TO_CKPT/sd-v1-4.ckpt" models/ldm/stable-diffusion-v1/model.ckpt
```


### Create conda environment

Create:

```sh
% CONDA_SUBDIR=osx-arm64 conda env create -f environment-mac.yaml
```

You should see output such as:

```txt
Collecting package metadata (repodata.json)
```

Restart your terminal.


### Activate

Activate:

```sh
% conda activate ldm
```


### Preload models

Preload python models:

```sh
% python3 scripts/preload_models.py
```

Heads up that the script does downloads that are somewhat large, more than 1GB.

You should set output such as:

```txt
preloading bert tokenizer...
preloading Kornia requirements ...
preloading CLIP model ...
```



### Run dream

Run:

```sh
% python3 scripts/dream.py --full_precision
```

You should see output such as:

```sh
* Initializing, be patient...
…
* Initialization done! Awaiting your command (-h for help, 'q' to quit)
dream> 
```

Note: we use the option `--full-precision`, and not the option `--half-precision`. This is because the option `--half-precision` requires autocast and won't work.



### Troubleshooting TypeAlias

If you get this error...

```txt
File "…/stable-diffusion/src/k-diffusion/k_diffusion/sampling.py", line 10, in <module>
    from typing import Optional, Callable, TypeAlias
ImportError: cannot import name 'TypeAlias' from 'typing' ("…/opt/anaconda3/envs/ldm/lib/python3.9/typing.py)
```

Then try editing this file:

```sh
src/k-diffusion/k_diffusion/sampling.py`
```

Change this line:

```python
from typing import Optional, Callable, TypeAlias
```

To:

```python
from typing import Optional, Callable
from typing_extensions import TypeAlias
```

➤ https://github.com/lstein/stable-diffusion/issues/302


### Generating

When you have the dream prompt:

```
dream>
```

Then you can enter your own command such as:

```sh
"photography of a cat on the moon" -s 20 -n 3 --sampler k_euler -W 384 -H 384
```

You should see output such as:

```txt
Generating…
Outputs:
outputs/img-samples/000001.2080708373.png …
outputs/img-samples/000001.1839445463.png …
outputs/img-samples/000001.2463981689.png …
```

You might see warning messages that you can ignore for now:

```sh
…/stable-diffusion/ldm/modules/embedding_manager.py:152: 
UserWarning: The operator 'aten::nonzero' is not currently supported 
on the MPS backend and will fall back to run on the CPU. 
This may have performance implications.
```

Your output files are now ready in this directory:

```sh
outputs/img-samples
```


## Troubleshooting

Troubleshooting can start with running these command line diagnostics:

```sh
brew --version

python3 --version

cmake --version

git --version

conda --version

which conda

# This may take a while because it's searching your entire system
find / -regex '.*/bin/conda' -type f -perm +111 -print

# This may show unexpected results if you have more than one conda
CONDA_SUBDIR=osx-arm64 conda env create -f environment-mac.yaml

conda activate ldm

python3 scripts/dream.py --full_precision
```
