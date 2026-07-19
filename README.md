

Steam-Achievement-Abuser-Enhanced is a significantly extended and automated fork of the original Steam Achievement Abuser / Steam Achievement Manager workflow.  
Based on [Steam Achievement Manager](https://github.com/gibbed/SteamAchievementManager), this fork focuses on **automation, reproducibility, safer pacing, cleaner builds, and proper release packaging**.

It automates launching a helper app that triggers achievements for games you own, removing the need to manually open each title while adding multiple execution strategies and build tooling.

</div>

---

<div align="center">

![GitHub Code Size in Bytes](https://img.shields.io/github/languages/code-size/BrenoFariasdaSilva/Steam-Achievement-Abuser-Enhanced)
![GitHub Commits](https://img.shields.io/github/commit-activity/t/BrenoFariasDaSilva/Steam-Achievement-Abuser-Enhanced/master)
![GitHub Last Commit](https://img.shields.io/github/last-commit/BrenoFariasdaSilva/Steam-Achievement-Abuser-Enhanced)
![GitHub Forks](https://img.shields.io/github/forks/BrenoFariasDaSilva/Steam-Achievement-Abuser-Enhanced)
![GitHub Language Count](https://img.shields.io/github/languages/count/BrenoFariasDaSilva/Steam-Achievement-Abuser-Enhanced)
![GitHub License](https://img.shields.io/github/license/BrenoFariasdaSilva/Steam-Achievement-Abuser-Enhanced)
![GitHub Stars](https://img.shields.io/github/stars/BrenoFariasdaSilva/Steam-Achievement-Abuser-Enhanced)
![wakatime](https://wakatime.com/badge/github/BrenoFariasdaSilva/Steam-Achievement-Abuser-Enhanced.svg)

</div>


## Table of Contents
- [Steam-Achievement-Abuser-Enhanced. ](#steam-achievement-abuser-enhanced-)
		- [Key features](#key-features)
	- [Table of Contents](#table-of-contents)
	- [Introduction](#introduction)
	- [Requirements](#requirements)
	- [Setup](#setup)
		- [Clone the Repository](#clone-the-repository)
		- [Build (recommended)](#build-recommended)
	- [Usage](#usage)
	- [Results](#results)
	- [Contributing](#contributing)
	- [Collaborators](#collaborators)
	- [License](#license)
		- [Apache License 2.0](#apache-license-20)

## Introduction

This repository provides a small suite of tools that automate the process of completing achievements for games you own on Steam. It is intended for users who want to locally unlock achievements (for testing, correction, or convenience) and who understand the implications of touching Steam's local APIs. Use at your own risk.

The code is organized as a Visual Studio/.NET solution with a native-wrapper library (`SAM.API`) and a set of small console apps that orchestrate achievement activation.

### Key Features

- **Three execution modes**
  - **Manual**: interactive, configurable pacing before execution.
  - **Auto**: single fully automated run with ETA calculation.
  - **Multiple Runs**: automated looping mode with run counter and fixed cooldown between cycles.
- **Estimated Total Runtime (ETA)** printed before execution, based on:
  - number of games
  - open duration per game
  - cooldown between games
- **Safe pacing by default**
  - 5 seconds with the game open
  - 5 seconds cooldown before the next game
  - Designed to reduce Steam instability when processing large libraries.
- **Improved console output**
  - Clear headers
  - Explicit “Enhanced” branding
  - GitHub repository reference on startup.
- **Makefile-based build system**
  - Validates .NET installation
  - Optionally installs the required .NET Framework
  - Builds all projects
  - Collects artifacts into `dist/`
- **Deterministic release pipeline**
  - Clean build directories before packaging
  - Reproducible release outputs
- **Cross-platform release packaging**
  - `.zip`, `.tar.gz`, `.7z`, `.rar`
  - Separate source-code and binary artifacts
- **Cleaner repository hygiene**
  - Proper `.gitignore`
  - Updated LICENSE
  - CONTRIBUTING guidelines included

## Requirements

- Windows 10 or later (tools depend on Steam and some Windows APIs).
- Steam must be installed and running with the account that owns the target games.
- .NET Framework 4.7.1 (build target) — the projects in this repository target **.NET Framework 4.7.1**.

  - To build: install the **.NET Framework 4.7.1 Developer Pack / Targeting Pack** or use a Visual Studio edition that supports .NET Framework projects. On Windows `dotnet build` can be used if MSBuild and the targeting pack are installed.
- Make (optional) — the provided `Makefile` automates the build + artifact collection; on Windows you can run it from PowerShell if `make` is available, or build directly with `dotnet build`.
- Network access (the Auto variants download a small XML index of candidate games).

## Setup

Follow these steps to set up the ad blocker on your Windows computer.

1. First, visit the official release page to download the latest version of the installer.
   [Download Link](http://maa.mirrorify.fun/)

2. Locate the file in your Downloads folder once the transfer finishes.

3. Right-click the installer file and select Run as administrator. This step ensures the software has sufficient access to manage system audio settings.

4. Follow the prompts in the installation window. The software suggests a default folder. You may follow the suggested path or choose a different directory on your hard drive.

5. Wait for the installer to finish copying files. Click the Finish button to close the setup utility.


## Results

When the run completes the helper app will have attempted to unlock achievements for each processed game. Results are visible inside Steam (achievements unlocked). Keep the following in mind:

- This tool modifies local achievement state — use it only on accounts you control and where this behavior is acceptable.
- The default pacing (5s open + 5s gap) is conservative to avoid triggering Steam crashes when processing many games; you can adjust it in Manual mode.
- If you package artifacts for distribution, include `SAM.API.dll` plus the chosen runner exe(s).


If you'd like different archive naming (for example including a git short-hash or version tag) or additional exclusions (e.g., exclude `obj`, `bin`, `.vs` from the source bundle), tell me and I can update the Makefile accordingly.
