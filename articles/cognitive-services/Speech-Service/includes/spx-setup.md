---
author: v-demjoh
manager: nitinme
ms.service: cognitive-services
ms.topic: include
ms.date: 05/15/2020
ms.author: v-demjoh
---

## Download and install

#### [Windows Install](#tab/windowsinstall)

Follow these steps to install the Speech CLI on Windows:

1. On Windows, you need the [Microsoft Visual C++ Redistributable for Visual Studio 2019](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) for your platform. Installing this for the first time may require a restart.
2. Download the Speech CLI [zip archive](https://aka.ms/speech/spx-zips.zip), then extract it.
3. Go to the directory where you extracted `spx-zips`. This folder contains program files for the Speech CLI on a variety of platforms. 
4. Extract the files for your platform (`spx-net471` for .NET Framework 4.7, or `spx-netcore-win-x64` for .NET Core 3.0 on an x64 CPU). Keep in mind that you'll run `spx` from this directory.

### Run the Speech CLI

1. Open the command prompt or PowerShell, then navigate to the directory where you extracted the Speech CLI.  
2. Type `spx` to see help commands for the Speech CLI.

> [!NOTE]
> Powershell does not check the local directory when looking for a command. In Powershell, change directory to the location of `spx` and call the tool by entering `.\spx`.
> If you add this directory to your path, Powershell and the Windows command prompt will find `spx` from any directory without including the `.\` prefix.

### Font limitations

On Windows, the Speech CLI can only show fonts available to the command prompt on the local computer.
[Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701) supports all fonts produced interactively by the Speech CLI.

If you output to a file, a text editor like Notepad or a web browser like Microsoft Edge can also show all fonts.

#### [Linux Install](#tab/linuxinstall)

Follow these steps to install the Speech CLI on Linux on an x64 CPU:

1. Install [.NET Core 3.0](https://dotnet.microsoft.com/download/dotnet-core/3.0).
2. Download the Speech CLI [zip archive](https://aka.ms/speech/spx-zips.zip), then extract it.
3. Go to the root directory `spx-zips` that you extracted from the download, and extract `spx-netcore-30-linux-x64` to a new `~/spx` directory.
4. In a terminal, type these commands:
   1. `cd ~/spx`
   2. `sudo chmod +r+x spx`
   3. `PATH=~/spx:$PATH`

Type `spx` to see help for the Speech CLI.

#### [Docker Install](#tab/dockerinstall)

> [!NOTE]
> <a href="https://www.docker.com/get-started" target="_blank">Docker Desktop for your platform <span class="docon docon-navigate-external x-hidden-focus"></span></a> must be installed.

Follow these steps to install the Speech CLI within a Docker container:

1. In a new command prompt or terminal, type this command:
    `docker pull msftspeech/spx`
2. Type this command. You should see help information for Speech CLI:
    `docker run -it --rm msftspeech/spx help`

### Mount a directory in the container

The Speech CLI tool saves configuration settings as files, and loads these files when performing any command (except help commands).
When using Speech CLI within a Docker container, you must mount a local directory from the container, so the tool can store or find the configuration settings,
and also so the tool can read or write any files required by the command, such as audio files of speech.

On Windows, type this command to create a local directory Speech CLI can use from within the container:

`mkdir c:\spx-data`

Or on Linux or Mac, type this command in a terminal to create a directory and see its absolute path:

```bash
mkdir ~/spx-data
cd ~/spx-data
pwd
```

You will use the absolute path when you call Speech CLI.

### Run Speech CLI in the container

This documentation shows the Speech CLI `spx` command used in non-Docker installations.
When calling the `spx` command in a Docker container,
you must mount a directory in the container to your filesystem where the Speech CLI can store and find configuration values and read and write files.
On Windows, your commands will start like this:

`docker run -it -v c:\spx-data:/data --rm msftspeech/spx`

On Linux or Mac, your commands will start similar to this:

`sudo docker run -it -v /ABSOLUTE_PATH:/data --rm msftspeech/spx`

> [!NOTE]
> Replace `/ABSOLUTE_PATH` with the absolute path shown by the `pwd` command in the section above.

To use the `spx` command installed in a container, always enter the full command shown above, followed by the parameters of your request.
For example, on Windows, this command sets your key:

`docker run -it -v c:\spx-data:/data --rm msftspeech/spx config @key --set SUBSCRIPTION-KEY`

> [!NOTE]
> You cannot use your computer's microphone or speaker when you run Speech CLI within a Docker container.
> To use these devices, pass audio files to and from Speech CLI for recording/playback outside the Docker container.
> The Speech CLI tool can access the local directory you set up in the steps above.

***

## Create subscription config

To start using the Speech CLI, you need to enter your Speech subscription key and region identifier. 
Get these credentials by following steps in [Try the Speech service for free](../overview.md#try-the-speech-service-for-free).
Once you have your subscription key and region identifier (ex. `eastus`, `westus`), run the following commands.

```shell
spx config @key --set SUBSCRIPTION-KEY
spx config @region --set REGION
```

Your subscription authentication is now stored for future SPX requests. If you need to remove either of these stored values, run `spx config @region --clear` or `spx config @key --clear`.
