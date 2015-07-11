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
---
The default parsing method for C# using current culture, which sucks really badly. ( I wrote about it on SO)

Here a lil helper  that I use

```c#
public static class Helper
{
	public static bool TryParseDouble(this TextBox textbox, out double value)
	{
		if (double.TryParse(textbox.Text, NumberStyles.Any, CultureInfo.InvariantCulture, out value))
		{
			textbox.Foreground = Brushes.Black;
			return true;
		}
		else
		{
			textbox.Foreground = Brushes.Red;
			return false;
		}
	}

	public static bool TryParseDouble(this string text, out double value)
	{
		return double.TryParse(text, NumberStyles.Any, CultureInfo.InvariantCulture, out value);
	}
}
```
