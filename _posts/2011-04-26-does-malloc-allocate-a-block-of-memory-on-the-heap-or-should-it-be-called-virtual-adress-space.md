---
layout: post
title: Does malloc allocate a block of memory on the heap or should it be called Virtual
  Adress Space?
date: 2011-04-26 13:19:28.000000000 +01:00
categories: []
tags:
- C#
- DOS
- Dynamic memory allocation
- Malloc
- Memory management
- Operating System
- Random-access memory
- Virtual Address Space
- Virtual Memory
status: publish
type: post
published: true
---


<p>To answer this question, we need to know what kind of <a class="zem_slink" title="Operating system" href="http://en.wikipedia.org/wiki/Operating_system" rel="wikipedia">Operating System</a> and architecture we are dealing with, the Standard and articles refers to “storage” or “space”. These are the most general terms and the only valid ones, unless we make a bunch of assumptions.</p>
<p>For example:</p>


<blockquote><p><a class="zem_slink" title="Malloc" href="http://en.wikipedia.org/wiki/Malloc" rel="wikipedia">malloc</a> allocates a block of <a class="zem_slink" title="Virtual address space" href="http://en.wikipedia.org/wiki/Virtual_address_space" rel="wikipedia">Virtual Address Space</a> on the heap</p></blockquote>
<p>This is not correct for many embedded systems. Many of them do not use <a class="zem_slink" title="Virtual memory" href="http://en.wikipedia.org/wiki/Virtual_memory" rel="wikipedia">Virtual Memory</a>, because there is no need (no multitasking etc.) or for performance reasons. What is more, it is possible that some exotic device does not have the idea of heap – doubt that malloc would be used, but fairly that is one of the reasons why the Standard refers to “storage” - it is implementation-specific.</p>
<p>On the other hand, the example is correct for Window and Linux in our <a class="zem_slink" title="Personal computer" href="http://en.wikipedia.org/wiki/Personal_computer" rel="wikipedia">PCs</a>. Let's analyze it to answer the question.</p>
<p>First off, we need to define what is Virtual Address Space.</p>
<p>Virtual Address Space (VAS) is a memory mapping mechanism that helps with managing multiple processes.</p>
<ul>
<li>isolate processes – each of them has his own address space</li>
<li>allow to allocate memory that 32-bit architecture is limited to.</li>
<li>provides one concise model of memory</li>
</ul>
<p>Back to question, ”Does malloc allocate a block of memory on the heap or should it be called Virtual <a class="zem_slink" title="Address space" href="http://en.wikipedia.org/wiki/Address_space" rel="wikipedia">Adress Space</a> ?”</p>
<p><strong>Both statements are correct</strong>. I would rather say <a class="zem_slink" title="Video Audio Project" href="http://www.vap.co.jp/" rel="homepage">VAP</a> instead of memory – it is more explicit. There is a common myth that malloc = <a class="zem_slink" title="Random-access memory" href="http://en.wikipedia.org/wiki/Random-access_memory" rel="wikipedia">RAM memory</a>. Back in old day, <a class="zem_slink" title="DOS" href="http://en.wikipedia.org/wiki/DOS" rel="wikipedia">DOS</a> <a class="zem_slink" title="Dynamic memory allocation" href="http://en.wikipedia.org/wiki/Dynamic_memory_allocation" rel="wikipedia">memory allocation</a> was very simple. Whenever we ask for memory it was always RAM, but in modern Oses it may vary.</p>
</div>
