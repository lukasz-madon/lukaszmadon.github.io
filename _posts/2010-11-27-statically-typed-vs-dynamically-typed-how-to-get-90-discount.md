---
layout: post
title: statically typed vs dynamically typed - How to get 90% discount.
date: 2010-11-27 21:57:09.000000000 +00:00
categories:
- Security
tags:
- Duck typing
- Floating point
- Programming
- Python
- shop
- Type system
- web
status: publish
type: post
published: true
meta:
  _edit_last: '17981463'
  _wp_old_slug: ''
author:
  login: soonstudios
  email: lukasz.madon@gmail.com
  display_name: Soon Studios
  first_name: ''
  last_name: ''
excerpt: !ruby/object:Hpricot::Doc
  options: {}
---
<p>There are a lot pros and cons of diffrent typing, yet on the one  hand static typing wins - security. Yes both can be more or  less secure buy <a class="zem_slink" title="Type system" rel="wikipedia" href="http://en.wikipedia.org/wiki/Type_system">static typing</a> tells you a lot about your code and prevents  from bugs, certain types of bugs. Do you want to buy a new flashy  notebook with 90% discount? Everybody does :)</p>
<ol>
<li>find a victim. Website with on-line shop.</li>
<li>Pick your laptop and start the order</li>
<li>In this process fill out the amount textbox with value '.1' (dot and one)</li>
</ol>
<p>Since most of the systems calculate the final value of bill :</p>
<p>ValueOfOneLaptop x AmountOfLaptops = TotalAmount</p>
<p>If there is no valiadtion upon <a class="zem_slink" title="Floating point" rel="wikipedia" href="http://en.wikipedia.org/wiki/Floating_point">floating point</a> TotalAmout will be 10%  of a laptop's value. How? .1 stands for 0.1 and therefore  0.1 gives you  90% discount :). Most likely shop engine is wirtten in <a class="zem_slink" title="PHP" rel="homepage" href="http://www.php.net/">PHP</a> or <a class="zem_slink" title="Python (programming language)" rel="homepage" href="http://www.python.org/">Python</a> so  you have a lot of chance to get it pass through. A shop employee  validates the order  and will not spot the little dot.</p>
<p>Brilliant isn't it?</p>
<p>Web Devs need to bare in mind this.</p>
<p>Static vs Dynamic 1:0.</p>
<p>Ps Cheating is bad mkay</p>
