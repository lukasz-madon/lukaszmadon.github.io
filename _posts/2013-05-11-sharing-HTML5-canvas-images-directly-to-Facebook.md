---
layout: post
title: Sharing HTML5 canvas images directly to Facebook
date: 2013-05-11 20:26:32.000000000 +00:00
categories:
- Javascript
tags:
- javascript
- canvas
- facbook
- api
---

TL;DR I made a small [web app](https://s3-us-west-2.amazonaws.com/www.heroesgenerator.com/index.html) that sends the content of HTML 5 canvas directly to Facebook, without intermediate storage. It converts canvas UrlData which is base64 to png and posts it to user's wall.

Do you pine the days of Heroes of Might and Magic III? :) Amazing game. A few days ago I stumble upon [a great post](http://blogging.alastair.is/how-i-served-100k-users-without-crashing-and-only-spent-0-32/) on Hacker News. I haven't use AWS before so I was curious to try it out. I wanted to make something a bit more sophisticated than a hello world app, then this idea of an event generator emerged (Game has a periodic events, usually with funny titles.).
 
![Picture](https://coderwall-assets-0.s3.amazonaws.com/uploads/picture/file/1607/heros.jpg)

*this one is not actually from the game*
 
I wanted to add a sharing for events. My first idea was to make a simple Heroku app that puts objects to S3. Amazon S3 is really a great tool, but can be very expensive (especially when you don't make money on it). Can I do better? Sure. I found [SO post](http://stackoverflow.com/a/5303242/945521) explaining how to convert canvas data to png and send it with XHR. The meritum is in `postCanvastoFacebook` function:

```javascript
function postCanvasToFacebook() {
  var data = canvas.toDataURL("image/png");
  var encodedPng = data.substring(data.indexOf(',') + 1, data.length);
  var decodedPng = Base64Binary.decode(encodedPng);
  FB.getLoginStatus(function(response) {
        if (response.status === "connected") {
```
and then depending on different statuses function calls `postImageToFacebook`

```javascript
postImageToFacebook(response.authResponse.accessToken, "heroesgenerator", "image/png", decodedPng, "www.heroesgenerator.com");

```
[Github](https://github.com/lukasz-madon/heroesgenerator)
