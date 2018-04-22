---
layout: post
title:  "The missing glut.h"
date:   2005-10-17
tags: OpenGL
---
Ref: http://fedora.redhat.com/projects/i18n/iiimf-faq.html

When compiling some OpenGL source files(e.g. Chap. 31 of Linux Programming Unleashing, 2nd Edition), you may be notified that the glut.h is missing! What can we do then? Install glut from http://www.opengl.org/resources/libraries/glut/glut_downloads.html? That may be a good solution, but that is time consuming. I found a link http://www.mcs.sdsmt.edu/csc433/GLUT/Linux/, where the glut.h and its corresponding library file libglut.a exist. Download those files and save libglut.a in /usr/lib, glut.h in /usr/include/GL. Ok just make, and you’ll get the correct bin file.
