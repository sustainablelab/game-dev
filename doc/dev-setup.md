% Setup Your Dev Tools
% Mike Gazes

# Doc history
January 20th, 2019: Start doc.
January 23rd, 2019: Visual Studio installer is like a package manager.

# Context
Epic Games supports development under Microsoft Visual Studio. The *free*
version is Microsoft Visual Studio Community 2017. This installs the necessary
build tools, but a lot of other stuff as well. That bothers a lot of people. It
bothered me.

But it turns out the Microsoft Visual Studio installer lets you
select what to install. At a minimum, you install the *core*, which is about
600MB. The core does not include a compiler. To get a compiler, you install one
of the pre-defined *workload* options, probably `Desktop development with C++`
or `Game development with C++`. You can also do a more granular install of
individual components.

To get the *leanest* set of tools, start with just the *core* and see if it has
what you need.

While not officially supported by Epic Games, community posts claim successful
set up of build tools without Microsoft Visual Studio. The most promising thread
I found was this one, describing a setup with Microsoft Visual Studio Code:
<https://answers.unrealengine.com/questions/761885/possibilities-of-coding-with-microsoft-visual-stud.html>

According to the post, Epic Games has some project-setup support for Microsoft
Visual Studio Code, a slim code editor environment that does not include any
build tools. Using Micrsoft Visual Studio Code lets me focus on the one battle
of adding a C++ compiler, so I am starting here instead of jumping straight to a
Vim setup. Once I have a working environment with Microsoft Visual Studio Code and the
Unreal Engine, I'll replace Microsoft Visual Studio Code with Vim.

I want to build my game for Windows, because all four of my computers, including
my very expensive VR rig, are running Windows as the primary OS, and it is what
my son is used to.

Up to now, my C dev work is ultimately for an embedded target. I only build on
my host Windows computer to run the test suite. This is not an *application* I
need to deploy to other computers. Anyone else running my test suite is going to
build the TestSuite.exe from source. Building the test suite on Windows makes it
sound like I already know how to compile C/C++ on Windows, but that is not the
case. I do all of this work in the POSIX environment provided by Cygwin. Such
executables do not run outside of Cygwin. A native Windows build (if I am even
saying this correctly) cannot be built from within Cygwin.

There are two choices: MinGW and MSVC (Microsoft Visual C++).

I get the sense that MinGW is a good choice for pure educational use. Third
parties will make sure they are compatible with MSVC and provide support to make
MSVC work. MinGW support is more spotty, and may not continue forever. I'd just
be opening myself up to more headaches in struggling to make my weirdo build
system.

MSVC is the right choice if I want to make a game that is going to run on other
computers.

# MSVC means many things
What is confusing is that MSVC is an IDE, not just a set of build tools. I think
this is where the community of hobbyists struggles. Microsoft is targeting
developers used to all-in-one solutions. Linux users, or weirdos like me who use
Cygwin, are used to composable utilities, patching them together for the unique
configuration that suits their needs. Neither approach is better, it always
depends on context. Windows users unfamiliar with the composable-utility
approach see this as death by a thousand tools. For the simplicity of installing
one tool, they are willing to let Microsoft dictate how they should work.

Microsoft recognizes that developers do not want to be locked into Microsoft
Visual Studio, so they modified the Visual Studio installer. The confusing bit
is that this only appears in a blog post. It does not appear prominently
anywhere on their download page. And of course any guidance from Microsoft or
Epic Games recommends people use Microsoft Visual Studio in its entirety. The
assumption is that you do not know how to build your own project from source and
you do not already have your own editor/IDE that you want to use.

So it turns out the Visual Studio installer acts similar to the Cygwin package
manager. It is an executable you run anytime to you want to modify your existing
installation. Start with the *core*. This is only 600MB. Then as you find you
need more, run the installer and select the components you need.

- `Game development with C++` takes 5.49GB, 2.7GB if you exclude the Windows 10
  SDK
    - included:
        - Visual Studio C++ core features
        - Windows Universal C Runtime
        - Visual C++ 2017 Redistributable Update
        - VC++ 2017 version 15.x latest v141 tools
    - optional:
        - C++ profiling tools
        - Windows 10 SDK
        - Cocos
        - Unreal Engine installer
        - Visual Studio Android support for Unreal Engine
- `Desktop development with C++` takes 5.83GB, 2.99GB if you exclude the Windows
  10 SDK, and 1.1GB if you exclude all of the optional items
    - included:
        - Visual Studio C++ core features
    - optional
        - Just-In-Time debugger
        - VC++ 2017 version 15.x latest v141 tools
        - C++ profiling tools
        - Windows 10 SDK
        - Visual C++ tools for CMake
        - Visual C++ ATL for x86 and x64
        - Test Adapter for Boost.Test
        - Test Adapter for Google.Test
- `Linux development with C++` takes 5.24GB
    - included:
        - Visual Studio C++ core features
        - Windows Universal C Runtime
        - Visual C++ for Linux Development
    - optional:
        - Visual C++ tools for CMake and Linux
        - Embedded and IoT Development

You can run Visual Studio with just the *core*. This is different from Visual
Studio Code, the lean text editor/IDE.

- [ ] determine if you can compile with just this, I suspect not

The next step up would be to select the `Desktop development with C++` and
remove all of the optional components.

- [ ] determine if you can compile with just this

# Tasks
- [ ] install Unreal Engine and Microsoft Visual Studio Code with C++ extension
- [ ] identify a suitable C++ compiler
- [ ] invoke the compiler from Microsoft Visual Studio Code
- [ ] build a small project using Unreal Engine and Microsoft Visual Studio Code
- [ ] build the same project using Unreal Engine and Vim
- [ ] identify a unit-test framework for C++
- [ ] automate unit-testing with Vim

# Installation
## Unreal Engine
1. Create an Epic Games account.
2. Run the installer for the Epic Games Launcher.
3. Sign into the Epic Games Launcher.
4. Click on *Unreal Engine* in the Epic Games Launcher and install the engine.
   This takes a while.
5. Launch the *Unreal Engine*.


## Microsoft Visual Studio Code and C++ extension
1. Download Visual Studio Code.
2. Install Visual Studio Code.
3. Run Visual Studio Code. Click *Extensions View* on left sidebar, find `c++`,
   click *Install*, click *Reload*.

## Chocolatey and Pandoc
I use Pandoc to generate HTML documentation from markdown. Install Pandoc with
Chocolatey.

### Chocolatey
1. Launch PowerShell as an Administrator and run this command:
```powershell
iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```
2. Restart PowerShell as non-Admin.
3. View Chocolatey help:
```powershell
choco /? | less
```
4. Surprisingly to me, Chocolatey also runs under Cygwin. One benefit of this
   is viewing help from the Cygwin installation of Vim.
   For example, `mintty` from PowerShell to open a bash terminal, then create a
   help file for the `install` command and open it in Vim:
```bash
choco install -help > choco-install.md
vim choco-install.md
```

### Pandoc
1. Run PowerShell as Administrator and install *pandoc* with this command:
```powershell
choco install pandoc
```
2. Generate HTML documentation:
```bash
pandoc -f markdown doc/dev-setup.md -s -o doc/dev-setup.html -c pandoc.css --toc
```
Note the style is included with `-c pandoc.css` and not `-c doc/pandoc.css`,
even though `pandoc.css` is in the `doc` folder.
