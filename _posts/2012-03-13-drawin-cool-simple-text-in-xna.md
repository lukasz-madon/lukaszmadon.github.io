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
---
I was wondering how to use some cool font in my XNA game. I came up with an idea to draw white and black text with an offset to give it "3d" look.

Here is the result:

![x](/images/text_xna.png)

I made extension methods for SpriteBatch  that write this kind of text

```csharp
public static class ExtensionMethods   
{      
  /// <summary>
  /// Draws white text with a black stroke
  /// </summary>
  public static void DrawStringBlackAndWhite(this SpriteBatch spriteBatch, SpriteFont smallFont, String text, Vector2 position)
  {
    spriteBatch.DrawStringWithStroke(smallFont, text, position, Color.White, Color.Black);
  }

  /// <summary>
  /// Draws white text with a black stroke
  /// </summary>
  public static void DrawStringBlackAndWhite(this SpriteBatch spriteBatch, SpriteFont smallFont, StringBuilder text, Vector2 position)
  {
    spriteBatch.DrawStringWithStroke(smallFont, text, position, Color.White, Color.Black);
  }

  /// <summary>
  /// Draws string with a stroke on up and right side of text
  /// </summary>
  public static void DrawStringWithStroke(this SpriteBatch spriteBatch, SpriteFont smallFont, String text, Vector2 position, Color color, Color stroke)
  {
    spriteBatch.DrawString(smallFont, text, position, stroke);
    spriteBatch.DrawString(smallFont, text, new Vector2(position.X - 1, position.Y + 1), color);
  }

  /// <summary>
  /// Draws string with a stroke on up and right side of text
  /// </summary>
  public static void DrawStringWithStroke(this SpriteBatch spriteBatch, SpriteFont smallFont, StringBuilder text, Vector2 position, Color color, Color stroke)
  {
    spriteBatch.DrawString(smallFont, text, position, stroke);
    spriteBatch.DrawString(smallFont, text, new Vector2(position.X - 1, position.Y + 1), color);
  }
}
```
