---
layout: post
title: Choosing Mocking for .NET
excerpt: "Choosing Mocking for .NET"
tags: [.NET, C#, Mock, Unit Tests, Unit testing, Mocking]
modified: 2015-12-21
comments: true
---

Statically-typed languages like C# offer developers benefits to build a solid and reliable design for all abstractions and if it compiles, it's already a half-way to be working.  
For other half of this road we need testing, and unlike manual or system testing in a specially prepared environment, developer can check a lot of stuff by writing atomic tests, called UnitTests, that do not require any envoronment or dependencies to execute and taht makes them fast and lightweight.  
Imagine you test a class, interacting with a web-service. And you don't want to set-up this web-service to test your code, or you even cannot do that due to platform, time or security limitations. So you make a stupid version of this service api, that returns predefined data for that.  
That is called a *Stub*  
While writing tests against this *Stub* you add functionality to record, how many calls you received to a particular address, or what parameters were passed, 
Your Stub becomes a *Mock*  

And following a golden DRY rool of programmers not to repeat themselves we come to a task of choosing a Mocking Framework, for which this article can be of help.

### obsoletion of **RhinoMocks** and mystery of **Microsoft Fake**
* * * 
First I have to say that the only major mocking library you should stay from is… a well known old-school Rhino Mocks. Because it is old in design and abandoned.  There was an attempt to resurrect it in 2014, and it seems to have failed. **v4** of RhinoMocks is still in alpha!  
{: .notice}

* [RhinoMocks NuGet](https://www.nuget.org/packages/RhinoMocks) - look at the number ov versions
* [RhinoMocks GitHub](https://github.com/RhinoMocks/RhinoMocks) – look at the starts and activity

Also [This nice article by *Jimmy Keen* ](http://jimmykeen.net/2014/12/13/mocking-frameworks-comparison/) - a guy with very high rep on StackOverflow for topics on UnitTesting states that you should not use RhinoMocks anymore:
>   Which framework you should stay away from? - RhinoMocks. Why?  
>       1. Its API is old, unpleasant and undocumented. It will make learning (it) harder and your tests will be more difficult to follow.  
>       2. It is no longer actively developed (regardless of recent attempts).  
>       3. It is one-man show (who might get bored and leave at some point).  
>       4. It is in alpha phase (since spring this year).

#### mystery of Microsoft **Fake**
There is also some strange library from Microsoft, called [Fake](https://msdn.microsoft.com/en-us/library/hh549175.aspx), but for Visual Studio Enterprise only – WTF ?!! I should research it better

### what to compare
* * * 
Meet the competitors: <a href="#FakeItEasy" class="btn">FakeItEasy</a> 
<a href="#Moq" class="btn btn-success">Moq</a> 
<a href="#NSubstitute" class="btn btn-warning">NSubstitute</a>

#### the argumens for choosing those three were the following
- They are actively developed
- They are on GitHub and have MIT or BSD license
- [Ninject](https://github.com/ninject/Ninject.MockingKernel) has extensions for these frameworks
- Already mentioned above [article by *Jimmy Keen*](http://jimmykeen.net/2014/12/13/mocking-frameworks-comparison/)
- Scores on [nugetmusthaves.com](http://nugetmusthaves.com/Tag/mocking)

##### Moq 
Open source, BSD license ( that means totally fine) 
* [Source code](https://github.com/Moq/moq4)
* Stats: 1064 stars, 276 forks, 16.6 on nugetmusthaves, downloads: ~5M
    * I’ve used it a lot, it’s totally cool
    * [This MSDN article](https://msdn.microsoft.com/en-us/data/dn314429.aspx) recommends it for EF6
##### NSubstitute
* [Source code](https://github.com/nsubstitute/NSubstitute)
* Stats: 536 stars, 123 forks, 12.7 on nugetmusthaves, downloads: ~700K 
* 
##### FakeItEasy
* [Source code](https://github.com/FakeItEasy/FakeItEasy)
* Stats: 462 stars, 96 forks, 8.2 on nugetmusthaves, downloads: ~300K

### popularity

| *property* | [Moq] | [NSubstitute] |  [FakeItEasy] |  
|:--------|:-------:|--------:|--------:|
| Stars on GitHub | 1064 |536 | 462|
| Forks                 | 276   | 123   | 96 |    
| Nugetmusthaves score  | 16.6    | 12.7    | 8.2 |   
| Downloads             | 5M    | 700K  | 300K | 
| License | BSD | BSD | MIT |

So clearly Moq is the most popular. And now about functionality

### functionality
Many articles including [this answer from *creator of FakeItEasy*](http://stackoverflow.com/a/4174495) states that the major differences are not in functionality, but in syntax and approach.

I am quite familiar with Moq only and love it. But actually the NSubstitute syntax I kind of like more, because you can mock methods without any lambdas. See the example:

{% highlight csharp %}
var serverMoq = new Mock<IServerGateway>();

serverMoq.Setup(server => server.HasUpgrades()).Returns(true);
{% endhighlight %}

{% highlight csharp %}

var serverSubstitute = Substitute.For<IServerGateway>();

serverSubstitute.HasUpgrades().Returns(true);
{% endhighlight %}

{% highlight csharp %}

var serverFake = A.Fake<IServerGateway>();

A.CallTo(() => serverFake.HasUpgrades()).Returns(true);
{% endhighlight %}
