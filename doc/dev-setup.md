% Setup Development Tools
% Mike Gazes
% January 20th, 2019

# Context
Epic Games supports development under Microsoft Visual Studio. The *free*
version is Microsoft Visual Studio Community 2017. This installs the necessary
build tools, but a lot of other stuff as well.

While not officially supported by Epic Games, community posts claim successful
set up of build tools without Microsoft Visual Studio. The most promising thread
I found was this one, describing a setup with Microsoft Visual Studio Code:
<https://answers.unrealengine.com/questions/761885/possibilities-of-coding-with-microsoft-visual-stud.html>

According to the post, Epic Games has some project-setup support for Microsoft
Visual Studio Code, a slim code editor environment that does not include any
build tools. Using Micrsoft Visual Studio Code lets me focus on the one battle
of adding a C++ compiler, so I am starting here instead of jumping straight to a
Vim setup.

Once I have a working environment with Microsoft Visual Studio Code and the
Unreal Engine, I'll replace Microsoft Visual Studio Code with Vim.

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
