# Stable Diffusion: macOS install help

Stable Diffusion macOS install help guide for this setup:

* Apple MacBook Pro M1
 
* Apple macOS 12.5.1

* Homebrew 3.5.10

* Python 3.10.6
 
* cmake 3.24.1
  
* git 2.37.3

* rustc 1.63.0

* Anaconda 4.13.0


## Guide Goals

This guide is our notes about our preferred way of installing Stable Diffusion.

This guide is intentionally step-by-step, because we want to help more people be successful, including people who are trying these kinds of software installs for the first time.

This guide is intentionally using steps that help multiple macOS users on the same system, because we want this guide to be able to help people who share a computer, such as teachers and students in schools.
  
We welcome constructive feedback via GitHub issues, or pull requests, or email to joel@joelparkerhenderson.com.

Thanks to:

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
