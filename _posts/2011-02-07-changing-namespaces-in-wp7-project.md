---
layout: post
title: Changing namespaces in WP7 project
date: 2011-02-07 02:45:30.000000000 +00:00
categories:
- C#
- silverlight
- Windows Phone 7
- WP7
tags:
- C#
- level
- Silverlight
- Spirit level
- stackoverflow
- Windows Phone 7
- WP7
- XAML
status: publish
type: post
published: true
---
It seems that VS 2010 screws the project properties when namespaces are changed.

<p><a href="http://stackoverflow.com/questions/4915816/deployment-schema-problem">I posted it on SO.</a></p>
<p>And the solution is:</p>
<blockquote><p>Check the "Startup Object" in the project properties page. The sometimes  requires manually being set/corrected when the namespace of the app is  changed.</p></blockquote>
<p>Thx Matt ;)</p>
