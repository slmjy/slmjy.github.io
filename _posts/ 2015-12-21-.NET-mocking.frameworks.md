First I have to say that the only major mocking library you should stay from is… Rhino Mocks. Because it is old. And abandoned.

There was an attempt to resurrect it in 2014, and it failed, v4 is still in alpha! ([nuget](https://www.nuget.org/packages/RhinoMocks), [github](https://github.com/RhinoMocks/RhinoMocks) – look at the starts, activity and so on)

There is also some strange library from Microsoft, called [Fake](https://msdn.microsoft.com/en-us/library/hh549175.aspx), but for Visual Studio Enterprise only – WTF ?!!

So I stick with [FakeItEasy](https://github.com/FakeItEasy/FakeItEasy), [Moq](https://github.com/Moq/moq4) or [NSubstitute](https://github.com/nsubstitute/NSubstitute) according to several considerations

- They are actively developed

- They are on GitHub and have MIT or BSD license

- [Ninject](https://github.com/ninject/Ninject.MockingKernel) has extensions for these frameworks

- [This article](http://jimmykeen.net/2014/12/13/mocking-frameworks-comparison/) from some guy with high rep in StackOverflow states that we should use [FakeItEasy](https://github.com/FakeItEasy/FakeItEasy), [Moq](https://github.com/Moq/moq4) or [NSubstitute](https://github.com/nsubstitute/NSubstitute). Rhino Mocks are obsolete, as he says.

- Score on [nugetmusthaves.com](http://nugetmusthaves.com/Tag/mocking)

1) [Moq](https://github.com/Moq/moq4) – open source, BSD license ( that means totally fine) _Stats:_ 1064 stars, 276 forks, 16.6 on nugetmusthaves, downloads: ~5M

a. I’ve used it, it’s totally cool

b. [This MSDN article](https://msdn.microsoft.com/en-us/data/dn314429.aspx) recommends it for EF6

2) [NSubstitute](https://github.com/nsubstitute/NSubstitute) – open source, BSD license ( that means totally fine) _Stats:_ 536 stars, 123 forks, 12.7 on nugetmusthaves, downloads: ~700K

3) [FakeItEasy](https://github.com/FakeItEasy/FakeItEasy)– open source, MIT license ( that means totally fine) _Stats:_ 462 stars, 96 forks, 8.2 on nugetmusthaves, downloads: ~300K

So clearly Moq is the most popular. And now about functionality

Many articles including [this answer from creator of FakeItEasy](http://stackoverflow.com/a/4174495) state that the major differences are not in functionality, but in syntax and approach.

<table border="1" cellpadding="0" cellspacing="0">

<tbody>

<tr>

<td valign="top">

_[Moq](https://github.com/Moq/moq4)_

</td>

<td valign="top">

_[NSubstitute](https://github.com/nsubstitute/NSubstitute)_

</td>

<td valign="top">

_[FakeItEasy](https://github.com/FakeItEasy/FakeItEasy)_

</td>

</tr>

<tr>

<td valign="top">

_Stars_

</td>

<td valign="top">

1064

</td>

<td valign="top">

536

</td>

<td valign="top">

462

</td>

</tr>

<tr>

<td valign="top">

_Forks_

</td>

<td valign="top">

276

</td>

<td valign="top">

123

</td>

<td valign="top">

96

</td>

</tr>

<tr>

<td valign="top">

_Nugetmusthaves score_

</td>

<td valign="top">

96

</td>

<td valign="top">

12

</td>

<td valign="top">

8

</td>

</tr>

<tr>

<td valign="top">

_Downloads_

</td>

<td valign="top">

5M

</td>

<td valign="top">

700K

</td>

<td valign="top">

300K

</td>

</tr>

<tr>

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
