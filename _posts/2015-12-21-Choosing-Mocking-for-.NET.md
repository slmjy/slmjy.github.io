---
layout: post
title: Choosing Mocking for .NET
excerpt: "Choosing Mocking for .NET"
tags: [.NET, C#, Mock, Unit Tests, Unit testing, Mocking]
modified: 2015-12-21
comments: true
---
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
There is also some strange library from Microsoft, called [Fake](https://msdn.microsoft.com/en-us/library/hh549175.aspx), but for Visual Studio Enterprise only – WTF ?!!

### what to compare
* * * 
<div markdown="0"><a href="https://github.com/FakeItEasy/FakeItEasy" class="btn">FakeItEasy</a></div>
<div markdown="0"><a href="https://github.com/Moq/moq4" class="btn btn-success">Moq</a></div>
<div ><a href="https://github.com/nsubstitute/NSubstitute" class="btn btn-warning">NSubstitute</a></div>

- They are actively developed
- They are on GitHub and have MIT or BSD license
- [Ninject](https://github.com/ninject/Ninject.MockingKernel) has extensions for these frameworks
- Already mentioned above [article by *Jimmy Keen*](http://jimmykeen.net/2014/12/13/mocking-frameworks-comparison/)
- Scores on [nugetmusthaves.com](http://nugetmusthaves.com/Tag/mocking)

### introducing competitors

1) [Moq](https://github.com/Moq/moq4) – open source, BSD license ( that means totally fine) _Stats:_ 1064 stars, 276 forks, 16.6 on nugetmusthaves, downloads: ~5M

a. I’ve used it, it’s totally cool

b. [This MSDN article](https://msdn.microsoft.com/en-us/data/dn314429.aspx) recommends it for EF6

2) [NSubstitute](https://github.com/nsubstitute/NSubstitute) – open source, BSD license ( that means totally fine) _Stats:_ 536 stars, 123 forks, 12.7 on nugetmusthaves, downloads: ~700K

3) [FakeItEasy](https://github.com/FakeItEasy/FakeItEasy)– open source, MIT license ( that means totally fine) _Stats:_ 462 stars, 96 forks, 8.2 on nugetmusthaves, downloads: ~300K

### popularity
| *property* | [Moq](https://github.com/Moq/moq4) | [NSubstitute](https://github.com/nsubstitute/NSubstitute) | [FakeItEasy](https://github.com/FakeItEasy/FakeItEasy) |
| -
|  Stars on GitHub      | 1064  | 536   | 462   |
| Forks                 | 276   | 123   | 96    |
| Nugetmusthaves score  | 96    | 12    | 8     |
| Downloads             | 5M    | 700K  | 300K  |
|=====
| Foot1   | Foot2   | Foot3 | - |

So clearly Moq is the most popular. And now about functionality

### functionality
Many articles including [this answer from creator of FakeItEasy](http://stackoverflow.com/a/4174495) state that the major differences are not in functionality, but in syntax and approach.



<td valign="top">

_Syntax_

</td>

<td valign="top">

var serverMoq = new Mock<IServerGateway>();

serverMoq.Setup(server => server.HasUpgrades()).Returns(true);

</td>

<td valign="top">

var serverSubstitute = Substitute.For<IServerGateway>();

serverSubstitute.HasUpgrades().Returns(true);

</td>

<td valign="top">

var serverFake = A.Fake<IServerGateway>();

A.CallTo(() => serverFake.HasUpgrades()).Returns(true);

</td>

</tr>

</tbody>

</table>

I am quite familiar with Moq only and love it. But actually the NSubstitute syntax I kind of like more, because you can mock methods without any lambdas
