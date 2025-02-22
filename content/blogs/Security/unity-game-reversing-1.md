---
title: "Unity Game Reversing(1): Setup"
date: 2023-04-17T04:16:55+08:00
showToc: true
categories: ["security"]
tags: ['tutorials', 'unity', 'reversing', 'dotnet']
---

## Introduction

Recently I am trying to reverse engineering a simple Windows desktop game made with Unity. I took a look on some reference but found that the setup can be a bit frustrating. This post is attempting to make the setup clearer and more followable. Reference links are listed below.

## Tools

Our target is to decompile and debug the `Assembly-CSharp.dll` inside the folder `<game root folder>\<GANE_NAME>_Data\Managed\`, which contains custom code the game developer wrote, not the code of Unity or other frameworks. It is written in `C#`. We need the below tools:

1. [dnSpy](https://github.com/dnSpy/dnSpy/)
2. [dotPeek](https://www.jetbrains.com/decompiler/)
3. [(patched) de4dot](https://github.com/earnol/de4dot/tree/dotPeek)
4. Some files from official Unity

## Setup

If you got a `DEBUG` build of the game, you are lucky, you can skip almost all the steps below and just use `dnSpy` to decompile, debug and modify the code (discussed below). But if you are not insider of the game development team and the team is not stupid enough (or, unfortunately, didn't get enough sleep) to release a debug build to production, you will be dealing with a `RELEASE` build.

Fortunately, there is a way to tweak the release build to debug build.

### Step 1

Check the version of Unity of the game. Open the file `<game root folder>\<game name>_Data\globalgamemanagers.assets` with notepad, the version of Unity will be shown at the beginning.

![](/unity_reversing1/unity_version.png)

### Step 2

Go to `https://unity.com/releases/editor/archive` and download the correct version of Unity. Install it.

### Step 3

Go to `<Unity root>\Editor\Data\PlaybackEngines\windowsstandalonesupport\Variations\win32_development_mono` if the game is 32bit, otherwise go to `<Unity root>\Editor\Data\PlaybackEngines\windowsstandalonesupport\Variations\win64_development_mono`.

![](/unity_reversing1/mono.png)

- Copy `Data\Managed` folder to the corr. folder of the game.
- Copy `WindowsPlayer.exe` and `UnityPlayer.dll`. Rename to `<GAME_NAME>.exe`.
- Copy `<Unity root>\Editor\Data\MonoBleedingEdge\bin\mono-2.0-bdwgc.dl` to `<GAME_NAME>\MonoBleedingEdge`.
- Create of edit `boot.config` and ensure the line `player-connection-debug=1` presents.

### Step 4

Download [this de4dot fork](https://github.com/earnol/de4dot/tree/dotPeek) and compile it locally by Visual Studio.

### Step 5

Run `de4dot.exe -f Assembly-CSharp.dll -o <output dll location> -fpdb`. Remove the output `pdb` file.

### Step 6

Load the output dll into dotPeek.
- Right click on the output dll and select `Export to Project`
- Check the box `Create *.pdb file`
- Export

### Step 7

Run the following command:
`"%UNITY_MONO%\bin\mono.exe" "%UNITY_MONO%\lib\mono\4.5\pdb2mdb.exe" "<target_assembly_dll>"`
where `"%UNITY_MONO%` is equal to `<Unity root>\Editor\Data\MonoBleedingEdge`.

You will get a `.mdb` file. Now you can debug with `dnSpy` the dll located in the same folder.

## Reference

1. [Debugging Unity Games](https://github.com/dnSpy/dnSpy/wiki/Debugging-Unity-Games)
2. [Let's Play with Fire Wiki](https://wiki.fireundubh.com/unity/turning-a-release-build-into-a-debug-build)
3. [DotPeek PDB generation for assemblies without debug directory](https://stackoverflow.com/questions/31299157/dotpeek-pdb-generation-for-assemblies-without-debug-directory)
