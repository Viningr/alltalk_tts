# AllTalk TTS v2 BETA
This is the BETA of v2. To be clear, that means they may well be bugs, issues, missing/incomplete documentation, a variety of potential problems etc (This is what BETA refers to in the software world for those whom dont know). This means you may need a bit of technical know how to deal with things that could come up and should only continue if you feel comfortable with that.

Github **discussions** on the BETA are [here in the discussion board](https://github.com/erew123/alltalk_tts/discussions/245)

For **Issues/Bugs/Support**, please open an issue ticket [here in the issues area](https://github.com/erew123/alltalk_tts/issues)

**Please note, my available time has become VERY limited due to unexpected family commitments. So please DYOR and refer to the TTS manufacturer (listed in the interface) for issues with their TTS engines.**

#### If you are going to run the BETA, please read all the info below....

The BETA has been tested on Windows 11 and Lunux (Ubuntu). The Standalone installations `atsetup` **should** take care of everything for you, all the way through to having DeepSpeed up and running on both Windows and Linux.

Seperate from Standalone installations, installation within the Text-generation-webui Python environment should also work, however, I have had to various bits of code last minute and not had an opportuninty to deeply test this yet.

### Screenshots
Please go see [here](https://github.com/erew123/alltalk_tts/discussions/237)

### New Features include

- Multiple TTS engines. Currently XTTS, Piper, Parler and VITS. New engines are easy to install with some coding experience. In time I will add in all engine Coqui supports as they should be easy.
  - Each engine has its own custom settings
  - You can download the models for each engine within its settings area.
  - FYI there is no limit on how many XTTS models AllTalk will now find/work with.
- AllTalk starts up on 0.0.0.0, meaning it will bind to ALL available IP addresses. There is no setting its IP address any more.
- Updated Coqui TTS engine.
- XTTS multiple audio sample TTS generation to improve voice reproduction https://github.com/erew123/alltalk_tts/commit/b7aa3a7c5c8df260edede52dd1b31a7b40d9b202
- Gradio web interface (see the screenshots)
- Retrieval based Voice Conversion, AKA, RVC voice Pipeline, re-written to work on Python 3.11.
- TTS Generator will now use any TTS engine.
- Vastly updated API Suite. **V2 is not 100% compatable with v1. (See here for an explanation https://github.com/erew123/alltalk_tts/issues/166)**. 
  - New SillyTavern extension is included in the `/system/` folder.
  - New remote TGWUI extension if you want to run your TTS elsewhere from the AllTalk server.
- OpenAI compatable endpoint/API. Meaning this should work as an alternative endpoint with any software that can send a TTS generation request to OpenAI.
- Fully customisable API Settings. I have **NOT** tested any limits of any TTS engines.
- Multi Engine Manager (MEM) (Run Multiple TTS Engine instances simultaneously with a queue system). See [here for details](https://github.com/erew123/alltalk_tts/issues/63#issuecomment-2365329723)
- Updated Finetuning for XTTS models
- Audio Transcoding to about 6x formats (mp3, opus, etc)
- About 50 gradio interface themes if you arent happy with the standard Gradio one.
- Documentaton has been about 80% updated. Its built into the interface.
- Lots and lots of other things too numerous to mention.

There is a welcome screen that covers a few other bits, along with the built in documentation.

### To install the BETA build, read the notes below for the type of system you have, the read the Quick Setup section to perform the install.

---

### Windows Systems Requirements
Before installing AllTalk you will need to have or install the following:

- You need to install **Git** to clone Github repositories. [Instructions here](https://github.com/erew123/alltalk_tts/wiki/Install-%E2%80%90-WINDOWS-%E2%80%90-Git)
- You need to install **Microsoft C++ Build Tools** and **Windows SDK** for Python to function correctly. [Instructions here](https://github.com/erew123/alltalk_tts/wiki/Install-%E2%80%90-WINDOWS-%E2%80%90-Python-C-&-SDK-Requirements)
- You need to install **Espeak-ng** for multiple TTS engines to function. [Instructions here](https://github.com/erew123/alltalk_tts/wiki/Install-%E2%80%90-WINDOWS-%E2%80%90-Espeak%E2%80%90ng)

### Linux Systems
You need to install a few bits (depending on your Linux flavour), otherwise DeepSpeed will fail and some TTS engines not work. At your terminal type the following:
- **Debian-based systems** `sudo apt install libaio-dev espeak-ng ffmpeg gcc g++`
- **RPM-based systems** `sudo yum install libaio-devel espeak-ng ffmpeg gcc g++`

As mentioned, the **atsetup.sh** install for Standalone installations **should** install deepspeed automatically. 

TGWUI - If however you are wanting to install in TGWUI and you can look here for a simpler way to get DeepSpeed installed here https://github.com/erew123/alltalk_tts/releases/tag/DeepSpeed-14.2-Linux, however, after 20+ hours wrestling with the conda python toolkit installations (on Linux), it looks like Nvidia may have a fault in their installation that can break 6x of the symlinks in the conda environment folder. They are reasonably easy to fix **if needed** and the script in `/system/config/fixsymlinks.sh` **may** do it for you, though I havnt tested on every OS with every eventuality etc.

### Mac Systems
I do not have a Mac system personally, so cannot test things out. In theory, all the TTS engines **should** work on Mac, however Ive been unable to write an installation routine for AllTalk. I have a loose idea of what to do. You would need to setup a miniconda for mac with Python 3.11.9 and Pytorch 2.2.1. You would need to install (brew) espeak-ng and ffmpeg (like Linux). I think at that point in time, once you have a working environment, you should be able to use the `requirements_standalone.txt` file with pip, though you may want to remove the nvidia cudnn bits, as mac cant use those. You would have to `conda install pytorch::faiss-cpu` and also `conda install conda-forge::ffmpeg`. The sticking point, if you wanted to use RVC is that you need a version of Fairseq that would work on Mac and Python 3.11.x. The only way I can think of doing that would be to compile a build of this https://github.com/VarunGumma/fairseq (if its possible), though I have no idea how to do that on a mac. So using RVC on Mac may be a no-no, or it may be possible for someone who wants to try figuring out Fairseq 12.2+ on mac.

### ALL Systems - General requirements
When I say general requirements, this is what I have tested it on. If you vary outside of this setup, expect issues. I will not have time to figure out why it doesnt work on Python version x and Pytorch version x, I dont have the resource/time available.<br>
- **Python version** 3.11.9<br>
- **PyTorch version** 2.2.1 with CUDA 12.1<br>
- **Standalone Installation Disk space** Used **during** installation may go as high as **23GB** of space. This is cleared down at the end of installation. Windows users can expect about 12GB of disk space before you install any models. Linux users can expect about 16GB of space, due to the extra need for the CUDA Toolkit.<br>
- **TGWUI Installation Disk Space** Will add about 2-3 GB onto the TGWUI Python environment.<br>

---

### 🟩 Quick Setup (Text-generation-webui & Standalone Installation)

Quick setup scripts are available for users on Windows 10/11 and Linux. Instructional videos for both setup processes are linked below.

- Ensure that **Git** is installed on your system as it is required for cloning the repository. If you do not have Git installed, visit [**Git's official website**](https://git-scm.com/downloads) to download and install it.
- **Important**: Do not use dashes or spaces in your folder path (e.g. avoid `/my folder-is-this/alltalk_tts-main`) as this causes issues with Python.

#### **NOTE. IF YOU HAVE AN EXISTING ALLTALK INSTALL** this will want to create a folder called `alltalk_tts` so you will need to re-name your old `alltalk_tts` to something else OR put this in a different folder/location. 
#### **NOTE**. I am not saying this is a over-the-top of an old alltalk upgrade ATM. It needs the Python environment rebuilding, hence a fresh install is needed for now. 

---
#### Python/PIP has recently made changes to the package installer and I have/am doing what I can to keep the requirements files working, however, this is a complicated time to say the least as some external requirements change and this can cause installation issues. Please raise a ticket if you have an error that a module is missing.
---

<details>
<summary>QUICK SETUP - Text-Generation-webui</summary>
<br>

For a step-by-step video guide, click [here](https://www.youtube.com/watch?v=icn2XS5rUH8).

To set up AllTalk within Text-generation-webui, follow either method:

1. **Download AllTalk Setup**:
   - **Via Terminal/Console (Recommended)**:
     - `cd \text-generation-webui\extensions\`
     - `git clone -b alltalkbeta https://github.com/erew123/alltalk_tts`

2. **Start Python Environment**:
   - In the text-generation-webui folder, start the environment with the appropriate command:
     - Windows: `cmd_windows.bat`
     - Linux: `./cmd_linux.sh`<br><br>
    
     > If you're unfamiliar with Python environments and wish to learn more, consider reviewing **Understanding Python Environments Simplified** in the Help section.

3. **Run AllTalk Setup Script**:
   - Navigate to the AllTalk directory and execute the setup script:
     - `cd extensions`
     - `cd alltalk_tts`
     - Windows: `atsetup.bat`
     - Linux: `./atsetup.sh`

4. **Install Requirements**:
   - Follow the on-screen instructions to install the necessary requirements. It's recommended to test AllTalk's functionality before installing DeepSpeed.

> **Note**: Always activate the Text-generation-webui Python environment before making any adjustments or using Fine-tuning. Additional instructions for Fine-tuning and DeepSpeed can be found within the setup utility and on this documentation page.

</details>

<details>
<summary>QUICK SETUP - Standalone Installation</summary>
<br>

For a step-by-step video guide, click [here](https://www.youtube.com/watch?v=AQYCccDRbaY).

To perform a Standalone installation of AllTalk:

1. **Get AllTalk Setup**:
   - **Via Terminal/Console (Recommended)**:
     - Navigate to your preferred directory: `cd C:\myfiles\`
     - Clone the AllTalk repository: `git clone -b alltalkbeta https://github.com/erew123/alltalk_tts`

2. **Start AllTalk Setup**:
   - Open a terminal/command prompt, move to the AllTalk directory, and run the setup script:
     - `cd alltalk_tts`
     - Windows: `atsetup.bat`
     - Linux: `./atsetup.sh`

3. **Follow the Setup Prompts**:
   - Select Standalone Installation and then Option 1 and follow any on-screen instructions to install the required files. DeepSpeed is automatically installed, but will only work on Nvidia GPU's.

> If you're unfamiliar with Python environments and wish to learn more, consider reviewing **Understanding Python Environments Simplified** in the Help section.

</details>

<details>
<summary>MANUAL Windows Setup - Standalone Installation</summary>
<br>

# Manual Windows Setup Instructions for AllTalk TTS

If for some reason the Quick Setup instructions above are not what you wish to do, you can follow these instructions to perform a manual installation.

## Prerequisites
1. Ensure you have curl installed on your system. If not, download and install it from https://curl.se/
2. Make sure your installation path does not contain spaces or special characters.
3. Install Microsoft C++ development tools for Python as detailed in [Windows & Python requirements for compiling packages here](https://github.com/erew123/alltalk_tts?tab=readme-ov-file#installation-and-setup-issues)
4. Ensure you have installed Espeak-ng as detailed above [here](https://github.com/erew123/alltalk_tts/tree/alltalkbeta?tab=readme-ov-file#windows-systems)

## Manual Installation Steps

#### If at any step you get an error code or message, you can retry that step or research on the internet what the error may be.

Error messages may vary, but could look like `('Connection broken: IncompleteRead(2742643 bytes read, 984095 more expected)', IncompleteRead(2742643 bytes read, 984095 more expected))` which would be a failure to fully download something from Conda (as an example). In such a situation you would re-try to the step or research on the internet, or even try later as it could be a transient fault.

These are **copy/paste** instructions, for Windows and you can click on the **double square button at the right of each step to copy it**. You then **right click with your mouse on the Command prompt** window to paste it in.

**Download AllTalk to your preferred folder**:
   - **Open a Windows Command Prompt from your Start Menu**:
     - Navigate to your preferred directory:
       ```
       cd C:\myfiles\
       ```
     - Clone the AllTalk repository:
       ```
       git clone -b alltalkbeta https://github.com/erew123/alltalk_tts
       ```

1. After cloning AllTalk into a folder, navigate into to the directory where you cloned AllTalk to.
   ```
   cd C:\myfiles\alltalk_tts
   ```

2. Create the alltalk_environment directory and navigate into it:
   ```
   mkdir alltalk_environment
   ```
   ```
   cd alltalk_environment
   ```

3. Download Miniconda:
   ```
   curl -Lk "https://repo.anaconda.com/miniconda/Miniconda3-py311_24.4.0-0-Windows-x86_64.exe" > miniconda_installer.exe
   ```

4. Install Miniconda:
   ```
   start /wait "" miniconda_installer.exe /InstallationType=JustMe /NoShortcuts=1 /AddToPath=0 /RegisterPython=0 /NoRegistry=1 /S /D=%cd%\conda
   ```

5. Navigate to the conda folder:
   ```
   cd conda
   ```

6. Create a new conda environment:
   ```
   .\condabin\conda create --no-shortcuts -y -k --prefix ..\env python=3.11.9
   ```

7. Activate the new environment:
   ```
   call .\condabin\conda.bat activate ..\env
   ```

8. Install PyTorch 2.2.1:
   ```
   .\Scripts\conda install -y pytorch==2.2.1 torchvision==0.17.1 torchaudio==2.2.1 pytorch-cuda=12.1 -c pytorch -c nvidia
   ```

9. Install Faiss:
   ```
   .\Scripts\conda install -y pytorch::faiss-cpu
   ```

10. Install FFmpeg:
    ```
    .\Scripts\conda install -y conda-forge::ffmpeg
    ```

11. Navigate back to the `alltalk_tts` folder where you cloned AllTalk to, then you can install requirements from the requirements file (adjust path as needed):
    ```
    cd..
    ```
    ```
    cd..
    ```
    You should now be back in your `alltalk_tts` folder e.g. `C:\myfiles\alltalk_tts`
    ```
    pip install -r system\requirements\requirements_standalone.txt
    ```

12. Update Gradio:
    ```
    pip install --upgrade gradio==4.32.2
    ```

13. Download and install DeepSpeed:
    ```
    curl -LO https://github.com/erew123/alltalk_tts/releases/download/DeepSpeed-14.0/deepspeed-0.14.0+ce78a63-cp311-cp311-win_amd64.whl
    ```
    ```
    pip install deepspeed-0.14.0+ce78a63-cp311-cp311-win_amd64.whl
    ```
    ```
    del deepspeed-0.14.0+ce78a63-cp311-cp311-win_amd64.whl
    ```

14. Install Parler:
    ```
    pip install -r system\requirements\requirements_parler.txt
    ```

Ignore the `ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
coqui-tts 0.24.1 requires transformers<4.41.0,>=4.33.0, but you have transformers 4.43.3 which is incompatible.` message


15. Clean the conda environment:
    ```
    .\alltalk_environment\conda\Scripts\conda clean --all --force-pkgs-dirs -y
    ```

16. Decide whether to downgrade transformers for XTTS streaming support:
    - If you want XTTS streaming support, run the following, ignoring the error message similar to the one on Step 14:
      ```
      pip install transformers==4.40.2
      ```
    - If you don't need XTTS streaming support, keep transformers at version 4.43.3.

Note: XTTS streaming may not work with versions of transformers other than 4.40.2.


# Detailed Guide to creating the AllTalk Batch Files

These batch files are used to start different parts of the AllTalk program. You'll need to edit them to match where you installed AllTalk on your computer.

## What You Need to Change

1. The parts of the script that points to the drive letter and the folder path to the `alltalk_tts` folder e.g. if your path was `C:\myfiles\alltalk_tts`, you would change `{drive_letter}:\{path_to_alltalk_folder}` to `C:\myfiles\alltalk_tts`
2. The Python script name at the end of some files

## Steps to Edit the Files

1. Open Notepad and create a file. You will insert the **Main Example** from below and change the `{drive_letter}:\{path_to_alltalk_folder}` to match your correct folder path.
2. Change all instances of `{drive_letter}:\{path_to_alltalk_folder}` to your AllTalk installation folder.
3. Add and change the Python script call name at the end of the file (except for start_environment.bat). (call's are detailed below)
4. Save the file with the correct file after making these changes and ensure they are BAT files and not TXT files.

## Main Example (for all files)

```batch
@echo off 
cd /D "{drive_letter}:\{path_to_alltalk_folder}\alltalk_tts\" 
set CONDA_ROOT_PREFIX={drive_letter}:\{path_to_alltalk_folder}\alltalk_tts\alltalk_environment\conda 
set INSTALL_ENV_DIR={drive_letter}:\{path_to_alltalk_folder}\alltalk_tts\alltalk_environment\env 
call "{drive_letter}:\{path_to_alltalk_folder}\alltalk_tts\alltalk_environment\conda\condabin\conda.bat" activate "{drive_letter}:\{path_to_alltalk_folder}\alltalk_tts\alltalk_environment\env" 
```

Replace `{drive_letter}` and `{path_to_alltalk_folder}` with your specific path.
For example: `C:\myfiles\alltalk_tts\`

## Specific Changes for Each File

After the common part above, each file (except start_environment.bat) has a line to run a Python script. Add the following line to the bottom of each file as follows:

### start_alltalk.bat
```
call python script.py 
```

### start_diagnostics.bat
```
call python diagnostics.py 
```

### start_finetune.bat
```
call python finetune.py 
```

### start_environment.bat
This file doesn't run a Python script, so no additional line is needed.

## Example of a Fully Edited File

Here's how `start_alltalk.bat` might look after editing, assuming `c:\myfiles\alltalk_tts` is the path you are using:

```batch
@echo off 
cd /D "C:\myfiles\alltalk_tts\" 
set CONDA_ROOT_PREFIX=C:\myfiles\alltalk_tts\alltalk_environment\conda 
set INSTALL_ENV_DIR=C:\myfiles\alltalk_tts\alltalk_environment\env 
call "C:\myfiles\alltalk_tts\alltalk_environment\conda\condabin\conda.bat" activate "C:\myfiles\alltalk_tts\alltalk_environment\env" 
call python script.py 
```

## Important Notes

- Make sure to keep the quotes (`"`) around the file paths.
- Don't change anything else in the files unless you're sure you know what you're doing.
- Ensure the files do not have a TXT extension on the name, but are Windows BAT files.
- After making these changes, the batch files should work correctly with your AllTalk installation.

</details>

---


### 🟪 Updating

As long as you did the `git clone` method to setup initially, you will be able to go into the folder and use `git pull` to download updates.

There was an issue with the `.gitignore` file, so if you cannot git pull on a build that is pre 11 June 2024, you can `git reset --hard origin/alltalkbeta` and then git pull (your config file will be reset).

---

### 🟨 Diagnostics Help with Issues/Start-up problems etc.

If you are having issues with starting AllTalk, it may well be because some of the 3rd Party packages versions have changed, or something is not right in your Python environment. Whilst its impossible to constantly ensure that everything is going to work perfectly, after installation, you can use the diagnostics tool to:

1) Generate a `diagnostics.log` file which contains information about your Python environment setup and performs various checks to ensure everything is installed.
2) Identify possible issues by comparing **your** `diagnostics.log` file to the **AllTalk base** `basediagnostics.log` stored in the `alltalk_tts/system/config/` folder.
3) Provide some semi-automated repair of your Python environment.

<details>
<summary>Expand here for instructions</summary>
<br>

### Starting diagnostics
Start the diagnostics from the `alltalk_tts` folder with either:

- **Windows:** `start_diagnostics.bat`
- **Linux:** `./start_diagnostics.sh`
- **TGWUI:** use TGWUI's cmd_{your_os} file
- **Other:** `python diagnostics.py` after starting **your** Python environment

You will be presented with a menu. The first thing you will need to do is generate your own diagnostics file, with option 1. This will create your `diagnostics.log` file in the `alltalk_tts` folder.

![image](https://github.com/erew123/screenshots/raw/main/gendiags1.jpg)
<br><br>
### Contents of the `diagnostic.log` file

You are welcome to look through this file and also check the on-screen output for failure notifications or package version issues.

![image](https://github.com/erew123/screenshots/raw/main/gendiags2.jpg)
<br><br>
### Comparing your `diagnostics.log` to the Standalone `basediagnostics.log`
Back at the main diagnostics menu, you can compare your `diagnostics.log` file to the `basediagnostics.log`file. This comparison will show any version differences between **your** Python environment and a tested working Python environment, as well as provide the commands to align your environment with the tested environment.

To do this comparison you will:

1) Select option 2 from the diagnostics menu and wait for the GUI to open.
2) Drag and drop `basediagnostics log` from the `/alltalk_tts/system/config` folder onto the **Base Diagnostics File** window.
3) Drag and drop **your** `diagnostics log` from the `/alltalk_tts/` folder onto the **Comparison Diagnostics File** window.
4) Click the **Compare the Base and Comparison log files** button.

You will now see a comparison of the **Base** and **Comparison** versions listed in chart form.

**Windows Users** note at the top of the GUI window, there are reference to Windows C++ Build Tools, Windows SDK and Espeak-ng. These are part of the base requirements and if missing you should install them as the installation of AllTalk's Python environment will have failed.

At the bottom of the GUI screen you will see:

- **Organised Results** this is the chart above, broken down into a text format and useful for quickly assessing what may be different from the base and useful if you need to create a issues ticket. Though the main thing required for a issues ticket is the `diagnostics.log` file.
- **Pip Commands to align versions** this list can either be copied to manually use at the command prompt/terminal window in **your** Python environment. Or, if you are in the AllTalk Python environment, you can use the **Run Pip commands** and that will install all updates to try match the versions. After doing this you can re-run the diagnostics, generate a new `diagnostics.log` and perform the compare again.

![image](https://github.com/erew123/screenshots/raw/main/gendiags3.jpg)
<br><br>
### Things this will not resolve or show

- **Corrupted packages or a corrupted Python Environment** You can always delete your Python Environment and start afresh. It may be worth clearing the PIP cache too (as below) before starting this process.
- **Corrupted files in your PIP download cache** Python caches installable packages so that you dont have to re-download them all the time. Sometimes these get corrupted or even sometimes, PIP will not update versions to newer versions when it finds there is already a copy in the PIP cache. You can clear the pip cache at your termina/command prompt window with `pip cache purge`
- **Corrupted Conda packages** There are 2x packages installed by Conda. In the **Standalone** installation of AllTalk, you can re-install these manually if you wish by:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- Running `start_environment` as necessary for your OS, from the `alltalk_tts` folder.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- `cd alltalk_environment`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- `cd conda`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- `cd scripts`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- `conda.exe install -y conda-forge::ffmpeg`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- `conda.exe install -y pytorch::faiss-cpu`
- **Other environmental factors I cannot account for**
<br><br>  
</details>

---

### 🆘 Support Requests, Troubleshooting, BETA Discussions & Feature requests
Current concerns with the v2 BETA are around, is this working and what needs doing to bring it or the documentation up to speed and not trying to introduce lots of additional features at this time. AKA, I want to make sure its stable etc.

If you wish to code something yourself though, thats perfectly to do and youre welcome to discuss that with me if needed.

General discussions on the BETA should be [here in the discussion board](https://github.com/erew123/alltalk_tts/discussions/245)

If you have a specifc technical problem, if you think its a quick/simple thing you can discuss it on the discussions board, however, if its a big issue or going to turn into one, lets keep that on an Issues ticket.

---
