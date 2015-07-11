---
layout: post
title: Usefull helper
date: 2011-12-07 18:12:47.000000000 +00:00
categories:
- C#
tags:
- C#
- Source code
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
<p>The default parsing method for C# using current culture, which sucks really badly. ( I wrote about it on <a href="http://stackoverflow.com/questions/6428670/how-to-fix-an-application-that-has-a-problem-with-decimal-separator">SO</a>)</p>
<p>Here a lil helper  that I use</p>
<p>[sourcecode language="csharp"]<br />
public static class Helper<br />
{<br />
public static bool TryParseDouble(this TextBox textbox, out double value)<br />
{<br />
if (double.TryParse(textbox.Text, NumberStyles.Any, CultureInfo.InvariantCulture, out value))<br />
{<br />
textbox.Foreground = Brushes.Black;<br />
return true;<br />
}<br />
else<br />
{<br />
textbox.Foreground = Brushes.Red;<br />
return false;<br />
}<br />
}</p>
<p>public static bool TryParseDouble(this string text, out double value)<br />
{<br />
return double.TryParse(text, NumberStyles.Any, CultureInfo.InvariantCulture, out value);<br />
}<br />
}<br />
[/sourcecode]</p>
