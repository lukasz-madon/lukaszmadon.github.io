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
<p>A few tips that make your life easer.</p>
<p><strong>General</strong></p>
<ol>
<li>Run your Visual Studio as an administrator (Right-click -&gt; run as administrator) to get better FPS.</li>
<li>Do not place IsTrial() in a loop. It take 60ms or more to return.</li>
<li>Code generation in the compact framework is not the same as  Windows' code. Jitter is optimized to run fast, not to produce the fastest code.</li>
<li>Property is just a function for .Net CF.</li>
</ol>
<p><strong>Emulator</strong></p>
<ol>
<li>To input text into emulator press Page-up (while editing a texbox f.e.) and then use your keybord to enter some text.</li>
<li>Use F9 and F10 to change the volume</li>
</ol>
<p><strong>Marketplace</strong></p>
<ol>
<li>To see app on marketplace if you are not from the country that has own  marketplace go to Control Panel -&gt; Location and change it to United  States.</li>
<li>Do not use transparent images at all!</li>
<li>http://stackoverflow.com/questions/4141186/tips-for-a-successful-windows-phone-7-marketplace-submission</li>
</ol>
<p><strong>Silverlight</strong></p>
<ol>
<li>Take as much as you can from Compositor Thread (for callback animations use BitmapCache).</li>
<li>Use Canvas or custom popup instead of default one (Popup class) - lack of hardware acceleration.</li>
<li>If your app loads very fast get rid off the spash screen.</li>
</ol>
<p><strong>XNA</strong></p>
<ol>
<li>Use DXT format for textures and pack them into 1 file (faster loading and fewer GPU texture switches).</li>
<li>For things like game stats avoid using strings( immutable). SpriteBatch.DrawString can take a StringBuilder directly for drawing text.</li>
<li>Avoid using/abusing LINQ and foreach (it <strong>may </strong>causes garbage).</li>
<li>Use Jagged arrays( arrays of arrays) instead of 2d arrays.</li>
</ol>
<p><a href="http://timheuer.com/blog/archive/2010/09/16/windows-phone-7-developer-tips-and-tricks.aspx">More info</a></p>
