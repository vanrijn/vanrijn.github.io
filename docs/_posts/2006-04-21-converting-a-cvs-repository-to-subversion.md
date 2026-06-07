---
layout: post
title: Converting a CVS Repository to Subversion
date: 2006-04-21 10:12:08.000000000 -07:00
published: true
categories:
- Open Source
- Work Stuff
tags: []
permalink: "/2006/04/21/converting-a-cvs-repository-to-subversion/"
---

I had thought that this would be a straight-forward mission, but it was not. While the front-end tools look and feel very much the same between [CVS](http://ximbiot.com/cvs/wiki/index.php?title=Main_Page) and [Subversion](http://cvs2svn.tigris.org/), the back ends are VERY different. Honestly, I much-prefer the CVS approach (all flat-files, predictably placed in $CVSROOT), but since that's probably part of the problem of CVS's lack of flexibility with file/directory moves, etc., it's understandable that Subversion does it differently.

Anyway, in using cvs2svn to convert my existing CVS repositories, I faced a problem that was covered in [cvs2svn's FAQ](http://cvs2svn.tigris.org/faq.html):more

> **How can I convert project foo so that trunk/tags/branches are inside of foo?**
>
>
> Given a CVS repository with the layout: /project_a /project_b
>
>
> cvs2svn will produce a Subversion repository with the following layout: trunk/ project_a/ ... project_b/ ... tags/ ... branches/ ...
>
>
> However, you may want your Subversion repository to be laid out like this: project_a/ trunk/ ... branches/ ... tags/ ... project_b/ trunk/ ... branches/ ... tags/ ...
>
>
> Currently, cvs2svn does not support converting a repository in this manner (see Issue #86 for details), however, there is a workaround. You can convert your repository one project (or module) at a time and load the individual dumpfiles into your Subversion repository using svnadmin with the --parent-dir switch. See the answer to How can I convert my CVS repository one module at a time? for details.

However, what I couldn't find was a script that would help me do this (of course, there's most probably one out "there" somewhere, but I didn't honestly have time to look that hard). So I created one and here it is:

```
#!/bin/bash

. ~/.profile.common

OLDCVSROOT=/home/cvsroot/blah
NEWSVNROOT=/home/svnroot/blah

CVS2SVNDIR=${HOME}/builds/cvs2svn-1.3.0

TMPCVSROOT=$(pwd)/tmpcvsroot
TMPWORKDIR=$(pwd)/tmpdir
TMPSVNDUMP=$(pwd)/tmpsvndumps

mkdir ${TMPCVSROOT}
mkdir ${TMPWORKDIR}
mkdir ${TMPSVNDUMP}

STARTDIR=$(pwd)

# create svn repository
# (commented out because this should be done before this process starts)
#svnadmin create --fs-type fsfs ${NEWSVNROOT}

for module in $(ls -1 --color=never ${OLDCVSROOT}| grep -v CVSROOT) ; do
module=$(basename $module)
echo "now working on module->$module< -"

# copy one module at a time (don't work on original repository)
mkdir ${TMPCVSROOT}/$module-root/
cp -r ${OLDCVSROOT}/CVSROOT ${TMPCVSROOT}/$module-root/
cp -r ${OLDCVSROOT}/$module   ${TMPCVSROOT}/$module-root/

# create an svn dump file from the copied CVS modulesitory/module
cd ${CVS2SVNDIR}
./cvs2svn -q --tmpdir=${TMPWORKDIR} --dump-only --dumpfile=${TMPSVNDUMP}/$module.dump ${TMPCVSROOT}/$module-root/$module
cd ${STARTDIR}

# create the parent directory in svn...
svn mkdir file://${NEWSVNROOT}/$module -m "Added $module directory."

# now load the dump into svn
svnadmin -q --parent-dir=$module load ${NEWSVNROOT} < ${TMPSVNDUMP}/$module.dump
done
```
