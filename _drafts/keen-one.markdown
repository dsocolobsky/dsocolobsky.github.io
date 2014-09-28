---
layout: post
title: "Keen Dreams Code Review: Part One"
date: 2014-03-19 17:40:41
---

I would like to start a series of blog posts, focusing on the analysis and review of opensource software.
First, I must mention I'm a begginer, therefore, expect some mistakes.

I decided to start by analizing "Keen Dreams", a recently opensourced game by idSoftware, and released back in 1992.
First, let's start by taking a look at the [github repo][kgithub].

By checking the [license][license], we see that the code is released under the GNU GPLv2 license, that's pretty neat.
On the "compiling" section, it is stated that the code is designed to be compiled under Borland C++ 2/3. Therefore, we will
need to do a bit more of work to get us started.

This is the list of software I had to install in order to build Keen Dreams:

* [Dosbox][dosbox]
* [Borland C++ 3.0][borland]
* [Keen Dreams Source Code][kgithub]

We will need DOSBOX in order to compile the game with Borland C++, and to run the game itself.

First, I created a folder in my C: drive called `keendreams`, I then created two folders inside it,
`C` and `D`, we will use this folders as mountpoints, the first for the HDD and the second for the game disk. 

I created a folder inside `keendreams\C` called `BC2`, I then unpacked the Borland C++ zip into said folder.
I also cloned the game's source code, and saved it into the `keendreams\D` directory:
`git clone https://github.com/keendreams/keen.git`

Finally I started DOSBOX, once you started you should be greeted by the `Z:\>` prompt, I then typed the following
commands to mount the drives:

```
Z:\> mount C C:\keendreams\C
Z:\> mount D C:\keendreams\D
```
We also need to adjust the PATH variable so that DOSBOX can find our Borland binaries:

`Z:\> SET PATH=Z:\;C:\BC2\BIN`

Now we can change into our D: drive in order to start compiling the game:

```
Z:\> D:
Z:\> cd keen\STATIC
Z:\> BC MAKEOBJ.C
```
This should open the following screen:
![Borland]({{site.url}})/assets/keen-bc.png)

Now press `F9`, 

[kgithub]: https://github.com/keendreams/keen
[license]: https://github.com/keendreams/keen/blob/master/LICENSE
[dosbox]: http://www.dosbox.com/
[borland]: http://monkey-hole.co.uk/esa/dos/
[buildblog]: http://x3ro.de/2014/09/18/keen-dreams-dosbox.html
