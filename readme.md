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

# Generate HTML documentation from markdown
In Vim, put the cursor in the window with the markdown file and do `;pan`.

Here is the shortcut to put in your .vimrc:
```vim
nnoremap <leader>pan :!pandoc -f markdown %:r.md -s -o %:r.html -c pandoc.css --toc<CR>
```

Or from a `bash` terminal, `cd` into `game-dev` and run the command:
```bash
pandoc -f markdown doc/readme.md -s -o doc/readme.html -c pandoc.css --toc
```

