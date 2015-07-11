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
meta:
  _edit_last: '17981463'
author:
  login: soonstudios
  email: lukasz.madon@gmail.com
  display_name: Soon Studios
  first_name: ''
  last_name: ''
excerpt: !ruby/object:Hpricot::Doc
  options: {}
---
<p>Silverlight for Windows Phone 7 is based on the page  navigation system. Key point is the lifetime of pages - each page is deleted while you navigate to another. To have an object(singleton f.e.) during the whole application life it could be placed in App class (App.xaml.cs file). MediaElement is definitely an object that should be one (there must be only one music player). The best and simple solution is place the MediaElement in XAML(it needs to be a part of visual tree), I have used application resources:</p>
<p>[sourcecode language="xml"]</p>
<p>&lt;!--Application Resources--&gt;<br />
&lt;Application.Resources&gt;<br />
   &lt;MediaElement x:Name=&quot;mediaPlayer&quot; Source=&quot;/Sound/horrorSong.mp3&quot; AutoPlay=&quot;False&quot;  /&gt;<br />
&lt;/Application.Resources&gt;<br />
[/sourcecode]</p>
<p>Then you can get it from any page:</p>
<p>[sourcecode language="csharp"]<br />
MediaElement player = null; // get the media element from App resources<br />
if (App.Current.Resources.Contains(&quot;mediaPlayer&quot;))<br />
{<br />
   player = App.Current.Resources[&quot;mediaPlayer&quot;] as MediaElement;<br />
}<br />
if (player != null)<br />
{<br />
   player.Play();<br />
}<br />
[/sourcecode]</p>
<p>MediaElement can't play the music while <a class="zem_slink" title="Zune" rel="wikipedia" href="http://en.wikipedia.org/wiki/Zune">Zune</a> is connect, it is good to prompt the user about it.</p>
<p>[sourcecode language="csharp"]<br />
if (NetworkInterface.GetIsNetworkAvailable())<br />
{<br />
   if (NetworkInterface.NetworkInterfaceType == NetworkInterfaceType.Ethernet)<br />
   {<br />
      zuneTextBlock.Visibility = System.Windows.Visibility.Visible;<br />
      return;<br />
   }<br />
}<br />
zuneTextBlock.Visibility = System.Windows.Visibility.Collapsed;<br />
[/sourcecode]</p>
<p>This code <strong>does not</strong> guarantee if Zune is on (User sill can have the plugged phone) but is very likely that Zune is running(Zune starts while you connect the phone).</p>
