---
layout: post
title: Drawin cool simple text in XNA
date: 2012-03-13 21:12:33.000000000 +00:00
categories: []
tags:
- C#
- game
- Programming
- SpriteBatch
- XNA
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
<p>I was wondering how to use some cool font in my XNA game. I came up with an idea to draw white and black text with an offset to give it "3d" look.</p>
<p>Here is the result:</p>
<p><a href="http://soonstudios.files.wordpress.com/2012/03/tlo2.png"><img class="size-full wp-image" src="assets/tlo2.png?w=199" alt="Image" /></a></p>
<p>I made extension methods for SpriteBatch  that write this kind of text</p>
<p>
[sourcecode language="csharp"]<br />
public static class ExtensionMethods   <br />
{       /// &lt;summary&gt;<br />
        /// Draws white text with a black stroke<br />
        /// &lt;/summary&gt;<br />
        public static void DrawStringBlackAndWhite(this SpriteBatch spriteBatch, SpriteFont smallFont, String text, Vector2 position)<br />
        {<br />
            spriteBatch.DrawStringWithStroke(smallFont, text, position, Color.White, Color.Black);<br />
        }</p>
<p>        /// &lt;summary&gt;<br />
        /// Draws white text with a black stroke<br />
        /// &lt;/summary&gt;<br />
        public static void DrawStringBlackAndWhite(this SpriteBatch spriteBatch, SpriteFont smallFont, StringBuilder text, Vector2 position)<br />
        {<br />
            spriteBatch.DrawStringWithStroke(smallFont, text, position, Color.White, Color.Black);<br />
        }</p>
<p>		/// &lt;summary&gt;<br />
		/// Draws string with a stroke on up and right side of text<br />
		/// &lt;/summary&gt;<br />
		public static void DrawStringWithStroke(this SpriteBatch spriteBatch, SpriteFont smallFont, String text, Vector2 position, Color color, Color stroke)<br />
		{<br />
			spriteBatch.DrawString(smallFont, text, position, stroke);<br />
			spriteBatch.DrawString(smallFont, text, new Vector2(position.X - 1, position.Y + 1), color);<br />
		}</p>
<p>		/// &lt;summary&gt;<br />
		/// Draws string with a stroke on up and right side of text<br />
		/// &lt;/summary&gt;<br />
		public static void DrawStringWithStroke(this SpriteBatch spriteBatch, SpriteFont smallFont, StringBuilder text, Vector2 position, Color color, Color stroke)<br />
		{<br />
			spriteBatch.DrawString(smallFont, text, position, stroke);<br />
			spriteBatch.DrawString(smallFont, text, new Vector2(position.X - 1, position.Y + 1), color);<br />
		}<br />
	}[/sourcecode]</p>
