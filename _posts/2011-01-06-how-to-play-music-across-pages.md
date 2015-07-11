---
layout: post
title: How to play music across pages.
date: 2011-01-06 02:06:10.000000000 +00:00
categories:
- C#
- silverlight
- Windows Phone 7
- WP7
tags:
- C#
- Extensible Application Markup Language
- media player
- MediaElement
- Multimedia
- Music and Audio
- Source code
- Windows Phone 7
- XAML
- zune
status: publish
type: post
published: true
---
Silverlight for Windows Phone 7 is based on the page  navigation system. Key point is the lifetime of pages - each page is deleted while you navigate to another. To have an object(singleton f.e.) during the whole application life it could be placed in App class (App.xaml.cs file). MediaElement is definitely an object that should be one (there must be only one music player). The best and simple solution is place the MediaElement in XAML(it needs to be a part of visual tree), I have used application resources:

```xml
<!--Application Resources-->
<Application.Resources>
<MediaElement x:Name="mediaPlayer" Source="/Sound/horrorSong.mp3" AutoPlay="False"  />
</Application.Resources>
```

Then you can get it from any page:
```xml
MediaElement player = null; // get the media element from App resources
if (App.Current.Resources.Contains("mediaPlayer"))
{
player = App.Current.Resources["mediaPlayer"] as MediaElement;
}
if (player != null)
{
player.Play();
}
```

MediaElement can't play the music while Zune is connect, it is good to prompt the user about it.

```c#
if (NetworkInterface.GetIsNetworkAvailable())
{
if (NetworkInterface.NetworkInterfaceType == NetworkInterfaceType.Ethernet)
{
zuneTextBlock.Visibility = System.Windows.Visibility.Visible;
return;
}
}
zuneTextBlock.Visibility = System.Windows.Visibility.Collapsed;
```

This code does not guarantee if Zune is on (User sill can have the plugged phone) but is very likely that Zune is running(Zune starts while you connect the phone).
