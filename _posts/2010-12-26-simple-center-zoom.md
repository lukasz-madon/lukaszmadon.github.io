---
layout: post
title: Simple center zoom
date: 2010-12-26 23:27:49.000000000 +00:00
categories:
- animations
- C#
- silverlight
tags:
- animation
- App Store
- Arts
- C#
- Filmmaking
- Illustration
- iPhone
- IPod Touch
- Microsoft Silverlight
- S
- Specialized
- Storyboard
- toolkit
- XAML
status: publish
type: post
published: true
---
To add simple pinch zoom (that I used in my Spirit Level) use the Silverlight Toolkit for WP7 and add the pinch GetureListener to a grid

```xml
<toolkit:GestureService.GestureListener>
<toolkit:GestureListener PinchDelta="GestureListener_PinchDelta" />
</toolkit:GestureService.GestureListener>
```

and code in event

```c#
private void GestureListener_PinchDelta(object sender, PinchGestureEventArgs e)
{
  if (e.DistanceRatio < 1.0 || e.DistanceRatio > 1.4)
  {
    return;
  }
  // Create the animation for pinch
  Storyboard storyboard = new Storyboard();
  DoubleAnimation pinchXAnimation = new DoubleAnimation();
  pinchXAnimation.To = e.DistanceRatio;
  pinchXAnimation.Duration = TimeSpan.FromSeconds(0.3);
  storyboard.Children.Add(pinchXAnimation);
  Storyboard.SetTargetProperty(pinchXAnimation, new PropertyPath("GridScaling.ScaleX"));
  Storyboard.SetTarget(pinchXAnimation, GridScaling);

  DoubleAnimation pinchYAnimation = new DoubleAnimation();
  pinchYAnimation.To = e.DistanceRatio;
  pinchYAnimation.Duration = TimeSpan.FromSeconds(0.3);
  storyboard.Children.Add(pinchYAnimation);
  Storyboard.SetTargetProperty(pinchYAnimation, new PropertyPath("GridScaling.ScaleY"));
  Storyboard.SetTarget(pinchYAnimation, GridScaling);

  storyboard.Begin();
}
```