---
published: true
title: Git Merge driver
layout: post
---
I want to use different diff/merge tools depending the extension of the file to work on.
In order to customize the behavior of Git in my repository, I have to add a file describing these path-specific settings.

Create a file name **.gitattributes** at the root of the working directory. So this file will be tracked by Git

ex:

```
# Specific diff
*.rpy  diff=Rhapsody
*.cmp  diff=Rhapsody
```

```
# Specific merge
*.rpy  merge=Rhapsody
*.cmp  merge=Rhapsody
```

Here I ask to Git to use the **merge driver** named *Rhapsody* when it has to merge or diff a file with extension .rpy or .cmp

Now, I will define this merge driver. I add it to the Git configuration, so **it is not tracked in your repository**.

```
git config --global --add diff.Rhapsody.name 'Rhapsody diff driver'
git config --global --add diff.Rhapsody.driver '/path/to/difftool %O %A %B'

git config --global --add merge.Rhapsody.name 'Rhapsody merge driver'
git config --global --add merge.Rhapsody.driver '/path/to/mergetool %O %A %B'
```

where tokens are replaced

* %O: ancestor's version  
* %A: current version
* %B: other branches version

To go further, see: [Official git attribute help](https://www.kernel.org/pub/software/scm/git/docs/gitattributes.html)
