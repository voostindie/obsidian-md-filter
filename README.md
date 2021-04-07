# Obsidian Marked Filter

Takes an Obsidian Markdown file and processes it for viewing in Marked. Set this script as a custom preprocessor in Marked to make it work.

What does the filter do? The main idea is that the output of the filter is a document that can live on its own, outside of an Obsidian vault. To achieve that, it: 

- Removes internal Obsidian links with just the text of the link.
    - `[[Link to other page]]` becomes `Link to other page`
    - `[[Link to other page|Alias]]` becomes `Alias`
- Replaces transclusions with IA Writer block syntax
    - `![[File to include]]` becomes `/path/to/File to include.extension`
    
In case the document being previewed is not in an Obsidian vault, this processor does nothing.

## Some notes on transclusions

- A transclusion only works if the instruction is on a single line, all by itself. Obsidian is more flexible, but Marked is not. And I don't want to rewrite the source content too much.
- Transclusions don't work if the referenced file doesn't exist or has multiple matches in the Obsidian vault.
- Transcluded files are not processed themselves. So, nested transclusion don't work. According to the Marked documentation it should work, but that's not my experience. I haven't looked into it further.
- I chose to use the IA Writer block syntax for three reasons:
    1. It has the cleanest syntax in my opinion.
    2. It works for many different file types.
    3. I use iA Writer myself, next to Obsidian, so I'm familiar with it.

## A note on Obsidian vaults

This filter looks for the vault the file being processed is in by locating the `.obsidian` folder in the directory structure, going upward from the current file. 

Since [version 0.11.13 of Obsidian](https://forum.obsidian.md/t/obsidian-release-v0-11-13/15900) the name of this folder is configurable, per vault. 

**This filter doesn't support that currently!**
