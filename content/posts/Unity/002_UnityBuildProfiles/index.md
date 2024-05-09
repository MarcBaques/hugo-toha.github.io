---
title: "Build Profiles: How to build with the new Unity 6"
date: 2024-05-08T08:06:25+06:00
description: Unity blog talking about new feature Build Profiles
menu:
  sidebar:
    name: Unity 6 Build Profiles
    identifier: unity_buildProfiles
    parent: unity
    weight: 10
hero: unity6.jpg
tags: ["Unity", "Builds", "Preview"]
---

> <b>Software used</b>: 
Unity 6 Preview, 6000.0f1 [Download](https://unity.com/releases/editor/whats-new/6000.0.0)

## First overlook
In the new version of Unity 6, or as we see in version 6000.0f1 there have been changes in the way of making builds, and so it is, Unity has added as they have called it the Build Profiles to be able to make different builds without having to be changing the parameters over and over again, let's play.

The first thing that caught my attention was that the Build Settings window has disappeared, now we have a window called Build Profiles. The shortcut to access it remains the same *Ctrl + Shift + B*.

![Build Profile window](/buildProfiles.png "Editor window")

This generates a big change when it comes to the methodology of making builds with Unity, we no longer have to modify Build Settings and Project settings depending on which build we want to make, now we will have profiles with those parameters.

Before making any question or trying to use it let's see what are build profiles.

___
## So what is a build profile?

Build profiles are scriptable objects that are stored in the folders *Assets/Settings/Build Profies* which contain the parameters of what used to be in Build Settings and Player Settings.
We have a list of default ones per platform and another list with our custom ones.

![Build Profile window](/buildProfiles_profileAsset.png "Editor window")

Each profile has a platform type and its parameters. You can create new ones, rename it and delete it with a context menu by right clicking it.

A build profile can be active or not, but only one can be active at all times. The active profile defines the platform you are on for Unity. 
To switch from one to another, you will see the Switch button at the top right if it is a non-active profile.
This means that switching between build profiles that have directive changes or platform changes will force us to recompile scripts and/or re-import assets to switch platforms.

#### Build Profiles sections
In the profiles we will find:
- A list of scenes, in case we want to modify the list of scenes we want to include in the build.
- A list of directives that will be added in the build to the ones we already have.
- A last section where you can override Player settings. Keep in mind that this is an override and can be undone at any time.

___
## Other consideration
There are some parts that don't quite work for me.
- On the top right we have the Asset Import Overrides option that we used to have in the Build Settings window. Now it's in a window that opens that button, which I'm not convinced by the change of position because it hides it a bit.
- We don't see any reference to Addressables in the profile either, with or without the Addressables package, the Addressables workflow remains unchanged it seems.

As for the active profile, this information seems to be stored in the user's own information, so the active one will not be shared in several machines, which seems to me to be the right thing to do.

___
## Build Profiles API
In terms of code they seem to have added the BuildProfile class along with two static functions, one that returns the active Build Profile and another to set the active BuildProfile.

So it seems that if we want to set another one as the active one we will have to use AssetDatabase to obtain the scriptableobjects and set the one we want to make a build. 

In automation systems we can simplify the logic because we only have to set as active the one we want and build.

___
## Changes I would like
- The addition of a searchable bar with filters for Build Profiles
- Some visual changes  due to the active tag of the Build Profile covering the name full name 
- Maybe the addition of Addressables profiles or something in the Build Profiles just if you have the Addressables package
- Adding a Switch Build Profile in Context Menu in the asset
- Maybe the option to enable/disable Pre/Post-processing scripts of Unity like IPreprocessBuildWithReport
- Not limiting the size of the name to the space in the editor window prevents you from being able to put very long but more descriptive names.

___
## My opinion
I'm looking forward to see if Unity is going to continue with these changes or leave it here, although it's true that I think it's already an improvement over what we were offered, I still think there could be more improvements with respect to builds with Addressables, with callbacks in the different steps of the builds that could be modified in the editor or other improvements that would further facilitate the builds for cross-platform development.

Unity references:
- https://docs.unity3d.com/6000.0/Documentation/Manual/BuildSettings.html 
- https://docs.unity3d.com/6000.0/Documentation/Manual/build-profiles-reference.html 
- https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Build.Profile.BuildProfile.GetActiveBuildProfile.html 
- https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Build.Profile.BuildProfile.SetActiveBuildProfile.html 

