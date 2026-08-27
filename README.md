# TinyEngine - Game Engine For Microcontrollers

<br />

<div align="center">
	<b>TinyEngine</b> - A game engine to turn your ESP32/Arduino into a mini retro game console! TinyEngine supports <b>TinyScript</b>, a high-level interpreted <b>custom scripting language</b> to allow you to make games on the fly without recompiling TinyEngine for your microcontroller. Inspired by the Game Boy and PSP.
</div>

## Demo

### Features

* **TinyEngine** 2D Game Engine
* **TinyScript** scripting language
* Console Emulation on PC


### TinyEngine
<div><video width="100px" align="center" src="https://github.com/user-attachments/assets/ec7205b4-f6b6-4be5-a814-8c1b3a0f6f02"></video></div>

### TinyScript

TinyScript is a high-level interpreted scripting language with its distinct BASIC-like syntax.

```
# Display Player in updated position
DEFINE FUNC0 BEGIN 
	M0 = M0 + (M1*JOYSTICK_X)/100

	# Bound player position
	IF M0-M3 < 0 THEN 
		M0 = M3
	ELSE IF M0+M3 > 319 THEN
		M0 = 319-M3
	END

	M63 = 0
	WHILE M63 < M2 DO 
		CALL LINE M0-M3, (239-M63), M0+M3, (239-M63), 255, 255, 255  
		M63 = M63 + 1
	END
END
```

### More Game Demos
<table>
  <tr>
    <td>
		<video align="center" src="https://github.com/user-attachments/assets/33827b4c-8e4e-426e-9b60-be744eea247d"></video>
    </td>
    <td>
      <video align="center" src="https://github.com/user-attachments/assets/da858756-d852-48f3-9bdf-db8580aac82f"></video>
    </td>
  </tr>
</table>

<br/>
<br/>

_Make sure to leave a GitHub star on this repo to show your support <3 :)_

<br />


>[!NOTE]
> The project is WIP!
> You can currently emulate and run the Game Engine on your laptop/computer.
> Future goals are to implement this on microcontrollers.

# Getting Started

The documentation for TinyScript lives under [Docs/README.md](Docs/README.md).

### TinyEngine Controls

<table>
	<tr>
		<th width="150px">Keys</th>
		<th width="300px">Description</th>
	</tr>
	<tr>
		<td>
			<kbd>W</kbd> / <kbd>A</kbd> / <kbd>S</kbd> / <kbd>D</kbd> or Arrow Keys
		</td>
		<td>
			Movement controls. emulates joystick, maps a keypress to -100%, 0% or 100% of equivalent joystick position.
		</td>
	</tr>
	<tr>
		<td>
			<kbd>E</kbd>
		</td>
		<td>
			Mapping to joystick click
		</td>
	</tr>
	<tr>
		<td>
			<kbd>O</kbd>
		</td>
		<td>
			Mapping to auxillary 'A' button
		</td>
	</tr>
</table>

# Installation

## Binary Releases

Install the binary releases [here](https://github.com/111nation/Arduino-Handheld-Console/releases) for your target Operating System. 

<details>
  <summary>Windows</summary>

Unzip the downloaded zipped file and run the project within the folder by double-clicking on it.

Alternatively, you can open a terminal window **within the root of the folder** and execute the following to run via the CLI.

```powershell
.\main.exe
```

 </details>

 <details>
  <summary>Linux (Unix)</summary>
  
Unzip the downloaded zip file by running the following in the same directory as the downloaded zip file.
```bash
unzip <Folder Name> .
cd <Folder Name>
```
To execute the binary via CLI, execute:

```powershell
./main
```
    
 </details>

 <details>
  <summary>MacOS</summary>
  
Unzip the downloaded zip file. You can do this by running the following in the same directory as the downloaded zip file.
```bash
unzip <Folder Name> .
cd <Folder Name>
```
Execute `main` within the unzipped folder or to execute the binary via CLI, execute:

```powershell
./main
```
    
 </details>
 

## Build From Source

Make sure you have the various prerequisites.

### Requirements
* C++ Compiler linked to your `PATH`
* CMake Version 3.23 or higher
* Make
* Git

### Building & Executing

> [!NOTE]
> Building commands may differ depending on your environment

Clone the repository onto your local system using the following.

```bash
git clone --recursive https://github.com/111nation/Arduino-Handheld-Console
```

Enter the cloned repository and enter the `GameEngine` directory to build and execute the Emulator.

```bash
cd Arduino-Handheld-Console
cd GameEngine

cmake -S . -B build
cmake --build build
```

## How TinyEngine Works

### Loading Games

When emulating the game engine on your personal computer, TinyEngine loads games from the programs folder, `$ROOT/programs/main`, where `$ROOT` is the current working directory of where TinyEngine was executed at. This currently functions as a basic bootloader for the game console to fetch the first instructions (which is just a single game at this point).

Depending if you downloaded a precompiled binary or built from source, `$ROOT` is the unzipped folder installed the precompiled binary or `$ROOT` is the `GameEngine` folder where cmake was executed.

Keep all custom-written games in `$ROOT/programs/`, 'load' a game by renaming it to `main` in the programs folder.

> [!TIP]
> Two sample games, a drawing and a pong game has been included as a demo


### TinyScript

This is the most fun part! This section is viewable at [Docs/README.md](Docs/README.md)


### Project Structure

<table>
  <thead>
    <tr>
      <th style="text-align: left;">Directory / Component</th>
      <th style="text-align: left;">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Depreciated/PyGameEngine</strong></td>
      <td>Stores the legacy, deprecated Python-based game engine codebase.</td>
    </tr>
    <tr>
      <td><strong>Arduino</strong></td>
      <td>Stores the Arduino implementation used to control physical hardware inputs.</td>
    </tr>
    <tr>
      <td><strong>GameEngine</strong></td>
      <td>Stores the main source code and data for the active game engine.</td>
    </tr>
    <tr>
      <td><strong>Docs</strong></td>
      <td>Contains the system and API documentation for the current game engine.</td>
    </tr>
  </tbody>
</table>
