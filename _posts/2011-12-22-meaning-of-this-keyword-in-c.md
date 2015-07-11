---
layout: post
title: Meaning of "this" keyword in C#
date: 2011-12-22 05:22:36.000000000 +00:00
categories:
- C#
tags:
- C#
- Source code
- this
status: publish
type: post
published: true
meta:
  _edit_last: '17981463'
  _oembed_cb04bfd75c74444fa6fe82961478e9a1: '{{unknown}}'
  _oembed_1f823d509249c06dbc0515b8cd18c964: '{{unknown}}'
  _oembed_17de250c5bcdf3746e01423b87a73540: '{{unknown}}'
  _oembed_7306aeac95c8c7b2fcee73b35af53689: '{{unknown}}'
  _oembed_14ed54d5e51b9415b7e969f3a9a4de34: '{{unknown}}'
  _oembed_3af6945f3984a67df3f0246785614c03: '{{unknown}}'
  _oembed_167dab3bfb20a163e6a1db22c75d8e2a: '{{unknown}}'
  _oembed_89e9c38ebe992bbcc1b1879024047ac3: '{{unknown}}'
  _oembed_e7eabbd88fa8a21e6f2f7edce349ba7f: '{{unknown}}'
  _oembed_4674747f276c1811425e47a33758fa9e: '{{unknown}}'
  _oembed_2fd122152406b3f6cee81e0fefb3deb3: '{{unknown}}'
  _oembed_bb32f42044f3ce1aff3e8f1fab8930f5: '{{unknown}}'
  _oembed_b28fef2495e929050622b494dd2107dd: '{{unknown}}'
  _oembed_565af890da00ff3b1be4cf7ec49bbb3e: '{{unknown}}'
  _oembed_dd0362d3080171b4cc2f0b2203b12ca7: '{{unknown}}'
  _oembed_78679638bbb97b9f792a2f6ac07b4374: '{{unknown}}'
  _oembed_052e8dc9ced887818dc8728937472323: '{{unknown}}'
  _oembed_5fb19105978f7c54e88f2ec1863413fb: '{{unknown}}'
  _oembed_95bba6047544bce1c53fcd236ca796b2: '{{unknown}}'
  _oembed_85a3c05493f3bf3114788220b9eeed78: '{{unknown}}'
author:
  login: soonstudios
  email: lukasz.madon@gmail.com
  display_name: Soon Studios
  first_name: ''
  last_name: ''
excerpt: !ruby/object:Hpricot::Doc
  options: {}
---
<p>Recently, I've been looking for all usages of "this" in C#. I couldn't find any good article, so I've "grepped" the spec.<br />
Surprisingly, I had wrong idea of "this" that is the same as in Java.</p>
<p>What is “this”? It is a keyword used in many object-oriented programming languages to refer to the current object. It can be implemented as a pointer (f.e. C++) or reference (f.e. Java), but in C# it has a few different meanings.</p>
<p><strong>Classes</strong></p>
<p>We can use “this” in 3 different context</p>
<p>-call other contructors</p>
<p>-refer to instance fields or methods</p>
<p>-pass current object</p>
<p>[sourcecode language="csharp"]<br />
public class Person<br />
{<br />
    private string name;<br />
    public Person()<br />
    {<br />
       name = &quot;John&quot;;<br />
    }</p>
<p>    public Person(string name)<br />
    : this() // call other constructor<br />
    {<br />
        // this is used to qualify the field<br />
        // “name” is hidden by parameter<br />
        this.name = name;<br />
    }</p>
<p>    public string Name<br />
    {<br />
        get { return name; }<br />
    }</p>
<p>    private void sayHi()<br />
    {<br />
        Console.WriteLine(&quot;Hi&quot;);<br />
        Foo.SayName(this); //use this to pass current object<br />
    }</p>
<p>    public void Speak()<br />
    {<br />
        this.sayHi(); // use this to refer to an instance method<br />
         Console.WriteLine(&quot;Want to come up and see my etchings? &quot;);<br />
    }<br />
}</p>
<p>class Foo<br />
{<br />
public static void SayName(Person person)<br />
{<br />
Console.WriteLine(&quot;My name is  {0}&quot;, person.Name);<br />
}<br />
}<br />
[/sourcecode]</p>
<p>&nbsp;</p>
<p><strong>Indexers</strong></p>
<p>Define an indexer for the type to have array-like semantics.</p>
<p>[sourcecode language="csharp"]<br />
public int this[int index]<br />
{<br />
    get { return array[index]; }<br />
    set { array[index] = value; }<br />
}<br />
[/sourcecode]</p>
<p><strong>Extension methods</strong><br />
[sourcecode language="csharp"]<br />
class Foo<br />
{<br />
     // with “this” modifiler we can use it like instance method of Person<br />
     public static void SayName(this Person person)<br />
     {<br />
          Console.WriteLine(“My name is  {0}”, person.Name);<br />
     }<br />
}<br />
 [/sourcecode]</p>
<p><strong>Structures</strong><br />
[sourcecode language="csharp"]<br />
struct MyVeryOwnInteger<br />
{<br />
    private int x;<br />
    public int Gimme()<br />
    {<br />
    // inside struct this is treated as a variable<br />
    // not reference to current structure<br />
    return this.x;<br />
    }<br />
}<br />
 [/sourcecode]</p>
<p>From the spe:</p>
<blockquote>
<h3><a name="_Ref450031207"></a>1.51.7This access</h3>
<p>A <span style="font-family:Times New Roman,serif;"><span style="font-size:x-small;"><em>this-access</em></span></span> consists of the reserved word <span style="font-family:Lucida Console,monospace;"><span style="font-size:x-small;">this</span></span>.</p>
<p lang=""><em>this-access:<br />
<span style="font-family:Lucida Console,monospace;"><span style="font-size:x-small;">this</span></span></em></p>
<p>A <span style="font-family:Times New Roman,serif;"><span style="font-size:x-small;"><em>this-access</em></span></span> is permitted only in the <span style="font-family:Times New Roman,serif;"><span style="font-size:x-small;"><em>block</em></span></span> of an instance constructor, an instance method, or an instance accessor. It has one of the following meanings:</p>
<p>When <span style="font-family:Lucida Console,monospace;"><span style="font-size:x-small;">this</span></span> is used in a <span style="font-family:Times New Roman,serif;"><span style="font-size:x-small;"><em>primary-expression</em></span></span> within an instance constructor of a class, it is classified as a value. The type of the value is the instance type (§1.89.1) of the class within which the usage occurs, and the value is a reference to the object being constructed.</p>
<p>When <span style="font-family:Lucida Console,monospace;"><span style="font-size:x-small;">this</span></span> is used in a <span style="font-family:Times New Roman,serif;"><span style="font-size:x-small;"><em>primary-expression</em></span></span> within an instance method or instance accessor of a class, it is classified as a value. The type of the value is the instance type (§1.89.1) of the class within which the usage occurs, and the value is a reference to the object for which the method or accessor was invoked.</p>
<p>When <span style="font-family:Lucida Console,monospace;"><span style="font-size:x-small;">this</span></span> is used in a <span style="font-family:Times New Roman,serif;"><span style="font-size:x-small;"><em>primary-expression</em></span></span> within an instance constructor of a struct, it is classified as a variable. The type of the variable is the instance type (§1.89.1) of the struct within which the usage occurs, and the variable represents the struct being constructed. The <span style="font-family:Lucida Console,monospace;"><span style="font-size:x-small;">this</span></span> variable of an instance constructor of a struct behaves exactly the same as an <span style="font-family:Lucida Console,monospace;"><span style="font-size:x-small;">out</span></span> parameter of the struct type—in particular, this means that the variable must be definitely assigned in every execution path of the instance constructor.</p>
<p>When <span style="font-family:Lucida Console,monospace;"><span style="font-size:x-small;">this</span></span> is used in a <span style="font-family:Times New Roman,serif;"><span style="font-size:x-small;"><em>primary-expression</em></span></span> within an instance method or instance accessor of a struct, it is classified as a variable. The type of the variable is the instance type (§1.89.1) of the struct within which the usage occurs.</p>
<p>If the method or accessor is not an iterator (§1.100), the <span style="font-family:Lucida Console,monospace;"><span style="font-size:x-small;">this</span></span> variable represents the struct for which the method or accessor was invoked, and behaves exactly the same as a <span style="font-family:Lucida Console,monospace;"><span style="font-size:x-small;">ref</span></span> parameter of the struct type.</p>
<p>If the method or accessor is an iterator, the <span style="font-family:Lucida Console,monospace;"><span style="font-size:x-small;">this</span></span> variable represents a <em>copy</em> of the struct for which the method or accessor was invoked, and behaves exactly the same as a <em>value</em> parameter of the struct type.</p>
<p>Use of <span style="font-family:Lucida Console,monospace;"><span style="font-size:x-small;">this</span></span> in a <span style="font-family:Times New Roman,serif;"><span style="font-size:x-small;"><em>primary-expression</em></span></span> in a context other than the ones listed above is a compile-time error. In particular, it is not possible to refer to <span style="font-family:Lucida Console,monospace;"><span style="font-size:x-small;">this</span></span> in a static method, a static property accessor, or in a <span style="font-family:Times New Roman,serif;"><span style="font-size:x-small;"><em>variable-initializer</em></span></span> of a field declaration.</p></blockquote>
<p>Yet another example that C# is not Java.</p>
