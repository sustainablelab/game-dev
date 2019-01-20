# Context
I want to learn game dev with my son. I have no prior experience with games or
C++, but I often develop embedded C and Python scripts for work.

The *Unreal Engine* is as good a starting point as any, except that it is
highly coupled to Microsoft Visual Studio, at least according to community
posts. My first goal is to set up a build tool without ever installing Microsoft
Visual Studio. Progress on this is documented in `doc/dev-setup.md`.

# Clone this repo
```bash
git clone https://github.com/sustainablelab/game-dev.git
```

# Generate documentation
Generate HTML documentation with `pandoc`:
```bash
pandoc -f markdown doc/dev-setup.md -s -o doc/dev-setup.html -c pandoc.css --toc
```
