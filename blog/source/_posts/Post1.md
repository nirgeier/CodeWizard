title: Post1
author: Nir Geier
date: 2020-02-16 03:17:37
tags:
---
### Let's start by explaining what a tag in git is

[![enter image description here][1]][1]

> A tag is used to label and mark a specific **commit** in the history.     
It is usually used to mark release points (eg. v1.0, etc.).

> Although a tag may appear similar to a branch, **a tag, however, does not change**. It points **directly** to a **specific commit** in the history.

[![enter image description here][2]][2]

----

You will not be able to checkout the tags if it's not locally in your repository so first, you have to `fetch` the tags to your local repository.

**First, make sure that the tag exists locally by doing**

    # --all will fetch all the remotes.
    # --tags will fetch all tags as well
    git fetch --all --tags --prune

**Then check out the tag by running** 

    git checkout tags/<tag_name> -b <branch_name>

Instead of `origin` use the `tags/` prefix.

---

In this sample you have 2 tags version 1.0 & version 1.1 you can check them out with any of the following:

    git checkout A  ...
    git checkout version 1.0  ...
    git checkout tags/version 1.0  ...

All of the above will do the same since the tag is only a pointer to a given commit.

[![enter image description here][3]][3]  
origin: https://backlog.com/git-tutorial/img/post/stepup/capture_stepup4_1_1.png

---
# How to see the list of all tags?

    # list all tags
    git tag

    # list all tags with given pattern ex: v-
    git tag --list 'v-*'
    
---

# How to create tags?

There are 2 ways to create a tag:
   
    # lightweight tag 
    git tag 
    
    # annotated tag
    git tag -a

The difference between the 2 is that when creating an annotated tag you can add metadata as you have in a git commit:  
name, e-mail, date, comment & signature  

[![enter image description here][4]][4]

# How to delete tags?

    # delete any given tag
    git tag -d <tag name>

    # Don't forget to remove the deleted tag form the server with push tags


# How to clone specific tag?

In order grab the content of a given tag you can use the `checkout` command. As explained above tags are like any other commits so we can use `checkout` and instead of using the SHA-1 simply replacing it with the *tag_name*

**Option 1:**

    # Update the local git repo with the latest tags from all remotes
    git fetch --all

    # checkout the specific tag
    git checkout tags/<tag> -b <branch>
    
**Option 2:**
### Using the clone command

Since git supports *shallow clone* by adding the `--branch` to the clone command we can use the tag name instead of the branch name. Git knows how to "translate" the given SHA-1 to the relevant commit

    # Clone a specific tag name using git clone 
     git clone <url> --branch=<tag_name>

> **git clone --branch=<name>**  
> 
> *`--branch` can also take tags and detaches the HEAD at that commit in the resulting repository.*


--------
# How to push tags?


###**`git push --tags`**

To push all tags:

    git push --tags 

To push annotated tags and current history chain tags use::

###**`git push --follow-tags`**

This flag `--follow-tags` pushes both **commits** and **only tags** that are both:

- Annotated tags (so you can skip local/temp build tags)
- Reachable tags (an ancestor) from the current branch (located on the history)

[![enter image description here][5]][5]

From Git 2.4 you can set it using configuration 
    
    git config --global push.followTags true

---------

Cheatsheet: 
[![enter image description here][6]][6]

-----


  [1]: https://i.stack.imgur.com/yRIIc.png
  [2]: https://i.stack.imgur.com/Xy20U.png
  [3]: https://i.stack.imgur.com/X4lvg.png
  [4]: https://i.stack.imgur.com/EwBtF.jpg
  [5]: https://i.stack.imgur.com/qLEtr.png
  [6]: https://i.stack.imgur.com/xR2sf.png