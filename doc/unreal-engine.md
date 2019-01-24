% Unreal Engine
% Mike Gazes
% January 20th, 2019

# First time
Start the Unreal Engine for the first time. It is a project management
environment with lots of templates for getting started, divided into tabs
*Blueprint* for starting game dev without C++, and *C++* for diving immediately
into C++.

Unreal Projects default to the Windows User's Documents folder:
`C:\Users\mike\Documents\Unreal Projects`

with the name:
`MyProject.uproject`

# No C++ Compiler Found
It seems that Unreal does not see the g++ package installed under Cygwin.

I can see it is visible from Windows by opening a PowerShell:
```powershell
which g++
```
this returns the path to `g++.exe`:
```bash
usr/bin/g++
```
which means the path to `g++.exe` is `C:\cygwin64\bin\g++.exe`.

Checking my path variable, I see the first item in my path is `C:\cygwin64\bin`.
So why doesn't Unreal see `g++`, my C++ compiler?

I cannot edit any settings without creating a project, and I cannot create a
project with a *C++* template because Unreal does not know where to find my C++
compiler.

First, create a project with a *Blueprint* template.
