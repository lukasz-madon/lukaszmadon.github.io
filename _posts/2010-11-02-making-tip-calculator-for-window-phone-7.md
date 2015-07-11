---
layout: post
title: Making Tip Calculator for Window Phone 7
date: 2010-11-02 20:26:32.000000000 +00:00
categories:
- Windows Phone 7
tags:
- animation
- C#
- codeplex
- Metro
- mobile
- phone
- Silverlight
- Source code
- UX
- Windows
- WP7
status: publish
type: post
published: true
---

TL;DR To try out WP7 tools I made [Tip Calcuator](http://tipcalc.codeplex.com/)

The so-called business logic is very simple and is not very different among various versions of Tip Calcs out there. Yet, what I would like to show is my way of [Metro UX](http://en.wikipedia.org/wiki/Metro_Design_Language) which I do believe is still a part of family.

A few interesting bits: When Textboxes are pressed, they move up and down.

```xml
<Storyboard  x:Name="mainInAnimation">
  <DoubleAnimation Storyboard.TargetName="ContentPanel"
   Storyboard.TargetProperty="(UIElement.RenderTransform).(CompositeTransform.TranslateX)"
    Duration="0:0:1" To="-20" >
    <DoubleAnimation.EasingFunction>
      <ExponentialEase  EasingMode="EaseOut"  />
    </DoubleAnimation.EasingFunction>
  </DoubleAnimation>
 <DoubleAnimation Storyboard.TargetName="TitlePanel"
   Storyboard.TargetProperty="(UIElement.RenderTransform).(CompositeTransform.TranslateX)"
   Duration="0:0:1" To="-20" >
   <DoubleAnimation.EasingFunction>
     <ExponentialEase  EasingMode="EaseOut"  />
    </DoubleAnimation.EasingFunction>
 </DoubleAnimation>
 <DoubleAnimation Storyboard.TargetName="ContentPanel"
    Storyboard.TargetProperty="Opacity" Duration="0:0:1.5" To="1">
    <DoubleAnimation.EasingFunction>
      <QuadraticEase EasingMode="EaseOut"  />
     </DoubleAnimation.EasingFunction>
    </DoubleAnimation>
</Storyboard>
```

## Styling 

I have made a few changes to the default style.

- opacity of TexBox is 0.7
- different margins (careful with that and bear in mind the rule of thumb - [0.9mm](http://channel9.msdn.com/Blogs/Jaime+Rodriguez/Windows-Phone-Design-Days-Target-Sizes)
- alignment 
- theme aware styles (like PhoneTextLargeStyle)

That is all about XAML, now C#.

```c#
public MainPage()
{
   InitializeComponent();
   this.LayoutUpdated += new EventHandler(MainPage_LayoutUpdated);
}
```

The ctor is kept light-weight for faster start of the app. All the details are handled by `MainPage_LayoutUpdated` event handler.

```c#
private void MainPage_LayoutUpdated(object sender, EventArgs e)
{
    if (m_onNavigatedToCalled)
    {
        m_onNavigatedToCalled = false;
        Dispatcher.BeginInvoke(() =>
        {
                Random random = new Random();
                var number = random.Next(1, 3);
                string fileName = String.Format(@"Images\background{0}.jpg", number);
                backgroundBrush.ImageSource = new BitmapImage(new Uri(fileName, UriKind.Relative));
                radioButton3.IsChecked = true;
                mainInAnimation.Begin();
        });
     }
}
```

Since we need to prepare things when everything is loaded `MainPage_LayoutUpdated` is a proper event, but it's called every time when layout has been updated, hence `m_onNavigatedToCalled` flag is set to true and after first call it's set to false. `Dispatcher.BeginInvoke` is a thread-safe asynchronous method for UI changes (mainly). In lambda expression the random background is picked and animation begins (I prefer do it in code).

## Orientation.
```c#
private void PhoneApplicationPage_OrientationChanged(object sender, OrientationChangedEventArgs e)
{
    if ((e.Orientation & PageOrientation.Portrait) == PageOrientation.Portrait)
    {
        Grid.SetRow(bottom, 1);
        Grid.SetColumn(bottom, 0);
        sumStackPanel.Margin = new Thickness(35, 30, 0, 0);
    }
    else
    {
        Grid.SetRow(bottom, 0);
        Grid.SetColumn(bottom, 1);
        sumStackPanel.Margin = new Thickness(-5, 30, 0, 0);
    }
}
```

To keep UI concise I have divided main Grid into 2 columns and 2 rows. After `OrientationChanged` event occurs bottom grid is set to next column. For the orientation changes the <a href="http://blogs.msdn.com/b/delay/archive/2010/09/28/this-one-s-for-you-gregor-mendel-code-to-animate-and-fade-windows-phone-orientation-changes-now-supports-a-new-mode-hybrid.aspx">Hybrid</a> animation do a nice job.

That is all interesting things about code.<strong> Here you can download the solution</strong> <a href="http://hotfile.com/dl/83013028/ca2e326/TipCalc.zip.html">link</a> OR 

And here is a demo. (animations are a bit choppy because of emulator + recording software) ;)
<iframe width="420" height="315" src="https://www.youtube.com/embed/3MNSn15ZefE" frameborder="0" allowfullscreen></iframe>

Feedback and comments are welcome.
