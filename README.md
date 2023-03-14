# WoZSim documentation


# Overview

**WoZSim** is a tool to allow HMI Prototype Evaluation in Wizard of Oz Experiments. It enables interactions captured in VR with prototype interfaces and/or other agents to be recorded and played back to enable post-analysis. WoZSim has been tested with Oculus Quest 2, tethered to a PC via Oculus Link connection. Make sure that your device has hand tracking enabled.
It is built on top of the [Ultimate Replay 2.0](https://assetstore.unity.com/packages/tools/camera/ultimate-replay-2-0-178602) (**UR**) asset from Unity's Asset Store.

Extending WoZSim requires knowledge of UR. See UR's user guide and samples for more information.

See a video of an earlier version of WoZSim [here](https://drive.google.com/file/d/14I3H60u8w3ewDkKpN1TuqM-na5cMjiOR/view?usp=sharing).

# Installation instructions

1. Do one of the following:
    * Add this repository as a git submodule in your Unity project, inside the Assets folder. 
    * Or, clone this repository and copy into your Assets folder.
2. Install the required packages and assets, see _Requirements_ below.
3. Follow the _Workflow_ instructions below for integrating WoZSim into your project

# Requirements

## Software
The following assets are required for WoZSim:

- [Ultimate Replay 2.0](https://assetstore.unity.com/packages/tools/camera/ultimate-replay-2-0-178602) (paid) - tested with version 2.1.8
- [Oculus Integration](https://assetstore.unity.com/packages/tools/integration/oculus-integration-82022)  - tested with version 33.0

The WoZSim Sample Project comes with the Oculus Integration but users must bring their own version of Ultimate Replay 2.0 into any project using WoZSim.

### Unity Editor
WoZSim has been developed and tested with Unity 2020.3 (LTS). The exact version is 2020.3.17f, but more recent 2020.3 (LTS) versions should work fine.


# Limitations

- The .replay recordings must be opened in the same scene they were recorded in.

# Workflows

WoZSim is currently set up for recording and playing back a VR user with hand tracking enabled. The workflow below assumes the required packages and assets have been set up correctly.

To use WoZSim in your scene:

1. Drag the WoZSim prefab, in Prefabs folder, into your scene hierarchy. This nested prefab contains everything you need for a quick start. Once this prefab is in your scene you can record and playback your hand tracked VR avatar.

Old way (still works):
1. Drag all three prefabs in the Prefabs/Main folder into your scene hierarchy
    1. You must remove any existing OVRCameraRig, the WoZSim prefab will replace this
2. Set the WoZSimOVRCameraRig as the Rig Source reference in the WoZSimManager inspector

You should now be able to record and play using the controls as indicated on the screen.

For recording additional objects in your scene, follow UR's user guide and documentation.

# References

All public methods and properties are documented with XML tags. Documentation can be generated with DocFX, Doxygen etc.

## WoZSim (prefab)
This nested prefab contains the prefabs below, for the most convenient way, simply drag this prefab into your scene and you're good to go.

Other prefabs in Prefabs/Main can be used individually:

## WoZSimManager (prefab)
WoZSimManager contains public methods that can used to control recording and playback programamatically.

### WoZSimManager (script)

#### Public methods
- `BeginRecording()` : Begins recording
- `StopRecording()` : Stops current recording
- `ToggleRecording()` : Toggles the recording mode. If using a single input source for both begin/stop recording, then use this.
- `Play()` : Plays the currently loaeded recording. Only works if not recording.
- `Live()` : Regular live mode. Only works if not recording.
- `Open()` : Open a file dialog for loading a .replay file. Only works if not recording.

#### Properties
- `recordingPrefix` : String prefix for the file name. Use inspector, or property to set programmatically. For example, use to store session ID, user name, scene name etc., in the file name.
- `infoString` : String that contains information about active mode, name of file being recorded/played etc. It is frequently used by `WoZSimGUI` for displaying information on screen. Read only.

### WoZSimGUI
The WoZSimGUI prefab provides convenient recording and playback controls. It uses Unity's IMGUI which means that it doesn't show up in the view of the VR user.
WoZSimGUI visualizes the current state of the WoZSimManager (recording, playing etc.) using IMGUI labels. WoZSimGUI also includes timeline and playback controls.
- R: Start/stop recording. After stopping, it automatically goes to play mode and plays recording.
- P: Play the currently loaded recording. This can be the most recent recording or a recording loaded from file.
- L: Live view.
- O: Open .replay file containing a recording.

During recording, the user must stop recording before switching modes

## WoZSimOVRCameraRig (prefab)
This prefab replaces the regular OVRCameraRig (using custom hands for hand tracking). It has UR recording components on multiple game objects in the rig hierarchy, for recording the head pose and hand tracking data.

## WoZSimPlaybackCameraRig (prefab)
This is a simple rig showcasing how cameras are wired into the WoZSim process. You are not required to use this specific rig, any camera in the scene that renders to the corresponding render textures (see Camera1, Camera2, Camera3, as examples) will appear in the WoZSim playback.

# Samples

Sample scenes can be found within the Scenes folder. Currently the following samples are available:

## Simple VR
This sample shows how to use the main prefabs to record headpose and handtracking data, with keyboard recording controls and graphical overlay using WoZSimGUI.

See the  [WoZSim Sample Project](https://github.com/FAR-Lab/WoZSim-Sample-Project) for a ready-to-use project.


