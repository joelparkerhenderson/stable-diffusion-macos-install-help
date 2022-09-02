# Stable Diffusion: macOS install help

<p><img src="https://images.squarespace-cdn.com/content/v1/6213c340453c3f502425776e/0715034d-4044-4c55-9131-e4bfd6dd20ca/2_4x.png?format=960w"></p>

Stable Diffusion macOS install help is our guide for this kind of setup:

* [Stable Diffusion](https://stability.ai/blog/stable-diffusion-public-release) image generator
  
* [Apple macOS Monterey](https://www.apple.com/macos/monterey/) on MacBook Pro M1

* [Homebrew](https://brew.sh) package manager

* [Python](https://www.python.org) programming language
 
* [cmake](https://cmake.org) build automation
  
* [git](https://www.git-scm.com) source code manager

* [Rust](https://www.rust-lang.org) programming language

* [protobuf](https://developers.google.com/protocol-buffers) data structures
 
* [Anaconda](https://www.anaconda.com) data science platform


## Guide Goals

This guide is our notes about our preferred way of installing Stable Diffusion.

This guide is intentionally step-by-step, because we want to help more people be successful, including people who are trying these kinds of software installs for the first time.

This guide is intentionally using steps that help multiple macOS users on the same system, because we want this guide to be able to help people who share a computer, such as teachers and students in schools.
  
This guide is intentionally doing "kitchen sink" approach, because this can help people with more capabilities as they try Stable Diffusion.

We welcome constructive feedback via GitHub issues, or pull requests, or email to joel@joelparkerhenderson.com.


## Thanks

Thanks to many developers working on Stable Diffusion and help for it, and special thanks to:

➤ https://www.assemblyai.com/blog/how-to-run-stable-diffusion-locally-to-generate-images/

➤ https://github.com/lstein/stable-diffusion/blob/main/README-Mac-MPS.md


## Homebrew

Install:

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Verify:

```sh
brew --prefix
/opt/homebrew

brew --version
Homebrew 3.5.10
```


## Python

Install:

```sh
brew install python
```

Verify:

```sh
brew --prefix python
/opt/homebrew/opt/python@3.10

python3 --version
Python 3.10.6
```


## cmake

Install:

```sh
brew install cmake
```

Verify:

```sh
brew --prefix cmake 
/opt/homebrew/opt/cmake

cmake --version
cmake version 3.24.1
```


## git

Install:

```sh
brew install git
```

Verify:

```sh
brew --prefix git  
/opt/homebrew/opt/git

git --version
git version 2.37.3
```


## protobuf

Install:

```sh
brew install protobuf
```

Verify:

```
brew --prefix protobuf
/opt/homebrew/opt/protobuf
```


## Rust

Install:

```sh
brew install rust
```

Verify:

```sh
brew --prefix rust
/opt/homebrew/opt/rust

rustc --version
rustc 1.63.0
```


## Anaconda

Install:

```sh
brew install anaconda
```

Verify:

```sh
brew info --cask anaconda
==> anaconda: 2022.05 (auto_updates)
https://www.anaconda.com/
/opt/homebrew/Caskroom/anaconda/2022.05 (304.8MB)
…
```


### Script

Anaconda uses an installation script, and you must run it, such as:

```sh
sudo /opt/homebrew/Caskroom/anaconda/2022.05/Anaconda3-2022.05-MacOSX-arm64.sh
```


### License

Anaconda prompts you to agree to the license:

```sh
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

We prefer to install software inside our typical `opt` directory:

```sh
$HOME/opt/anaconda3
```

Type your own preferred installation directory, then return.


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

Verify the installation works by running Anaconda using its full path:

```sh
/opt/anaconda3/condabin/conda --version
conda 4.13.0
```


### Path

Optionally, you can append the Anaconda path to your environment, such as by editing any of these:

* `/etc/bashrc` 

* `/etc/zshrc`

* `$HOME/.bashrc` 

* `$HOME/.zshrc`

Export your preferred path such as:

```sh
export PATH="$PATH:$HOME/opt/anaconda3/condabin"
```

Restart your terminal, or source the path file, or equivalent.

After you add the Anaconda path, then you can verify it:

```sh
conda --version
conda 4.13.0
```

### Update

Update conda just in case it's changed recently:

```sh
conda update -n base -c defaults conda
```


## Stable Diffusion weights file

Download the Stable Diffusion weights file; heads up that the file is somewhat large, more than 4GB.

```sh
curl https://www.googleapis.com/storage/v1/b/aai-blog-files/o/sd-v1-4.ckpt?alt=media > sd-v1-4.ckpt
```

We prefer to put the file in its own directory so it's easier to access for all our macOS users:

```sh
sudo mkdir /opt/stable-diffusion-ckpt
sudo mv sd-v1-4.ckpt /opt/stable-diffusion-ckpt
```


## Stable Diffusion repository

This section comes from:

➤ https://github.com/lstein/stable-diffusion/blob/main/README-Mac-MPS.md


### Install

Install:

```sh
cd ~
git clone https://github.com/lstein/stable-diffusion.git
cd stable-diffusion
```


### Link

Link to the CKPT file:

```sh
mkdir -p models/ldm/stable-diffusion-v1/
PATH_TO_CKPT="/opt/stable-diffusion-ckpt"  # use your own directory that contains your CPKT file
ln -sfn "$PATH_TO_CKPT/sd-v1-4.ckpt" models/ldm/stable-diffusion-v1/model.ckpt
```


### Create conda environment

Create:

```sh
CONDA_SUBDIR=osx-arm64 conda env create -f environment-mac.yaml
```

You should see output such as:

```txt
Collecting package metadata (repodata.json)
```

Restart your terminal.


### Activate

Activate:

```sh
conda activate ldm
```


### Preload models

Preload python models:

```sh
python scripts/preload_models.py
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
python scripts/dream.py --full_precision  # half-precision requires autocast and won't work
```

You should see output such as:

```sh
* Initializing, be patient...
…
* Initialization done! Awaiting your command (-h for help, 'q' to quit)
dream> 
```


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

You might see warning message that you can ignore for now:

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
