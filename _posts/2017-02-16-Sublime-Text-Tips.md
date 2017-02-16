---
layout: post
title:  "Sublime Text (2) : Tips and Tricks"
date: 2017-02-16 09:00:00 +0530
categories: tips sublime
description: Tips and Tricks for Sublime Text...
---

# Sublime Text Tips

## Slow `Goto Anything` for large projects

- As you probably know, you can press `Ctrl+P` to open the `Goto Anything` search bar to take you to any file in the project
- Over very large projects this can get considerably slow.
- All you have to do is go to your `User Settings` and add this to exclude folders that you don't need Sublime to Parse.
    - For a Meteorjs project for example, you can happily exclude `.meteor` and `.build` directories to speed things up

```
"folder_exclude_patterns": [".svn", ".git", ".hg", "CVS"]
```
