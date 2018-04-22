---
layout: post
title:  "fstream in MFC"
date:   2005-12-08
tags: fstream
---
Strange enough. When using fstream in MFC, you have to write "#include <fstream>" in the header file xxxdoc.h. If you write that clause in the first line of xxxdoc.cpp, or in the last line of the "#include" area, you will get lots of errors that caused not by your own cpp files! The right place for "#include <fstream>", I think, is the line just above the line "#ifdef _DEBUG".
 
When you have to overwrite the member function OnSaveDocument of the document class, you have to delete the default return cluase, and return a TRUE. Or, nothing will be written in your output files.
 
MFC dose somewhat deviate from standard C++.
 
PS: ends causes some unregnized characters in the output file, while "\t" will not.
