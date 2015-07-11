---
layout: post
title: Tips about WP7
date: 2010-11-04 22:44:33.000000000 +00:00
categories:
- Windows Phone 7
tags:
- Emulators
- marketplace
- Microsoft
- Microsoft Silverlight
- Microsoft Visual Studio
- Microsoft XNA
- Programming
- Windows Phone 7
status: publish
type: post
published: true
---
A few tips that make your life easer.

## General

Run your Visual Studio as an administrator (Right-click -&gt; run as administrator) to get better FPS.
Do not place IsTrial() in a loop. It take 60ms or more to return.
Code generation in the compact framework is not the same as  Windows' code. Jitter is optimized to run fast, not to produce the fastest code.
Property is just a function for .Net CF.

## Emulator

To input text into emulator press Page-up (while editing a texbox f.e.) and then use your keybord to enter some text.
Use F9 and F10 to change the volume

## Marketplace

To see app on marketplace if you are not from the country that has own  marketplace go to Control Panel -&gt; Location and change it to United  States.
Do not use transparent images at all!
http://stackoverflow.com/questions/4141186/tips-for-a-successful-windows-phone-7-marketplace-submission

## Silverlight

Take as much as you can from Compositor Thread (for callback animations use BitmapCache).
Use Canvas or custom popup instead of default one (Popup class) - lack of hardware acceleration.
If your app loads very fast get rid off the spash screen.

## XNA

Use DXT format for textures and pack them into 1 file (faster loading and fewer GPU texture switches).
For things like game stats avoid using strings( immutable). SpriteBatch.DrawString can take a StringBuilder directly for drawing text.
Avoid using/abusing LINQ and foreach (it may causes garbage).
Use Jagged arrays( arrays of arrays) instead of 2d arrays.

[More info](http://timheuer.com/blog/archive/2010/09/16/windows-phone-7-developer-tips-and-tricks.aspx)
