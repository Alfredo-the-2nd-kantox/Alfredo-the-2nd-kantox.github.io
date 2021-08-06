---
layout: post
title: How to compare files between different branches
description:
date: 2021-08-01 09:35:00
image:
categories: git
tags: []
---

Changes that my_branch will incorporates relatively to the current state of the other_branch

    git diff other_branch my_branch -- path/to/file

equivalent to

    git diff other_branch..my_branch -- path/to/file

Changes that my_branch will incorporates relatively to the branching point from the other_branch

    git diff other_branch...my_branch -- path/to/file

Example

Current tree

    * 3b64c4b (master) commit 3 with line 5
    * b1e17f5 commit 2 with lines 3 and 4
    | * 724366b (HEAD -> branch-1) index again
    | * 94b005d index
    | * f207ce5 index 3
    |/
    * 4ea42be index-2
    * d02c1dc commit 1 with lines 1 and 2
    (END)

Changes relatively to the current state -> 2 dots notation (..)

    git diff master..branch-1  -- index.txt

    diff --git a/index.txt b/index.txt
    index a751413..5bb8407 100644
    --- a/index.txt
    +++ b/index.txt
    @@ -1,5 +1,5 @@
    -line 1
    -line 2     --> base of branch-1
    -line 3     --> commit 2
    -line 4     --> commit 2
    -line 5     --> commit 3
    \ No newline at end of file
    +Paragraph 1
    +  line 1
    +  line 2
    +  line 3
    +  line 4
    (END)

Changes from the branching point --> 3 dot notation (...)

    git diff master...branch-1  -- index.txt

    diff --git a/index.txt b/index.txt
    index 7bba8c8..5bb8407 100644
    --- a/index.txt
    +++ b/index.txt
    @@ -1,2 +1,5 @@
    -line 1
    -line 2
    +Paragraph 1
    +  line 1
    +  line 2
    +  line 3
    +  line 4
    (END)
