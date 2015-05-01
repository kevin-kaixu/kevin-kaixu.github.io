MeshStudio (version for Feature Curve Orientation)

By: Kai (Kevin) Xu
email: kevin.kai.xu@gmail.com
webpage: http://www.kevinkaixu.net/k/code/fast_code.html

***************************************************************************************************************

* Please cite the following papers if you use the source code:

Kai Xu, Daniel Cohen-Or, Tao Ju, Ligang Liu, Hao Zhang, Shizhe Zhou, and Yueshan Xiong,
"Feature-Aligned Shape Texturing," ACM Transactions on Graphics (SIGGRAPH Aisa 2009), 28(5).

Kai Xu, Hao Zhang, Daniel Cohen-Or, and Yueshan Xiong, "Dynamic Harmonic Fields for Surface Processing,"
Computers and Graphics (Special Issue of Shape Modeling International 2009), Vol. 33, pp. 391-398.

***************************************************************************************************************

* Copyright

MeshStudio is developed by Kai Xu for research use. All rights about the program (esp. feature curve orientation)
are reserved by Kai Xu. This C++ source codes are available only to a primary user for academic purposes. No
secondary use, such as copy, distribution, diversion, business purpose, etc., is allowed. In no event shall the
author be liable to any party for direct, indirect, special, incidental, or consequential damage arising out of
the use of this program. MeshStudio is built on top of CGAL and many other libraries and source codes (see the
copyright terms therein).

***************************************************************************************************************

* Download
The source code (MSVC++ 2005 project), as well as the testing data, from the homepage of Kai Xu:

http://sites.google.com/site/kevinkaixu/publications/fast/code

***************************************************************************************************************

* Compilation (Windows+MSVC2005)

To compile the MSVC++ 2005 project, you need to first install CGAL (version 3.3 is prefered) and BOOST which is
required by CGAL. In the following, I will use $(CGALROOT) referring to the root directory of CGAL, $(BOOSTROOT)
to that of Boost, and $(MeshStudio) to that of MeshStudio project.

The computation of harmonic vector field depends on CHOLMOD, so you also need to include/link CHOLMOD stuff.
All you need to do is simply copying the the headers in "cholmod.zip(\include)" into
"$(CGALROOT)\auxiliary\cholmod\include\" and the libs in "cholmod.zip(\lib)" into
"$(CGALROOT)\auxiliary\cholmod\lib\". The including and linking setting has been set up within the VS project.

I wrote a wrapper class for CHOLMOD matrix and vector (but not including the solver APIs) which you can
find in "cholmod_wrapper.zip". Copy the two .h files into "$(CGALROOT)\include\CGAL\".

***************************************************************************************************************

* Usage

A quick start usage can be:

1. Load mesh file: "File->Open Model", choose the file format (e.g. obj) to load fandisk.obj

2. Load its crest line file: "Crestline->Open & Proc", choose the format of crest line file

   There are two options. You can load either the output of Shin Yoshizawa's crest line program or the crest
   line processed and saved by MeshStudio.

   Yoshizawa's program (I attached a version compiled by myself in Windows) output two seperate files for
   ravines and ridges. Before loading them you should rename them by adding the same suffix for both of
   the file (the suffix should begin with '_' and the name can be arbitrary), for example, I rename them as
   ravines_fandisk.txt and ridges_fandisk.txt for the fandisk model.

   Note that in the file open dialog, you can choose any one of the two files and MeshStudio will load the
   other oneautomatically. Since the crest lines could be not perfect (e.g., break at unexpected position,
   or too many short curves), you may need to modify them by using the filtering and modification function
   provided by MeshStudio. A dialog will pop out after file loading, with which you can proceed to do the
   modification and orientation optimization. Please see the image $(MeshStudio)\manual.png as an intuitive
   instruction on how to use the functions.

   If you already got your own feature curves for the model (say, using other program), you should output
   the curves in either Yoshizawa's format (see http://www.riken.jp/brict/Yoshizawa/Research/Crest.html for
   definition) or my Cleaned Crest Line format (.ccl). The CCL format is straightforward. Please see the
   explanation at the end of this document.

   Curve orientation optimization can be performed any time no matter what data you have loaded. The
   vector field corresponding to the optimized orientation will also be computed.

3. At any time, you can save your processed and/or orientation-optimized curves into CCL file for future use.
   You can also save the computed vector field into file (*.shvf).

***************************************************************************************************************

* Format of CCL File

Take the given file fandisk.ccl for example:

6371						// number of points
6334						// number of segments
37						// number of curves
-0.013652 -0.539497 -0.28183 0			// list of points: 
-0.013566 -0.53925 -0.281224 0			// (X-coord, Y-coord, Z-coord, Ic)
-0.014061 -0.538851 -0.28087 0			//	* -coord is the location coordinates of the point
-0.0127 -0.539958 -0.281819 0			//	* Ic is the index of curve to which the point belongs
... ...
86.2881 0.974288 3603.91 1			// list of curves:
73.8592 0.974188 1554.84 1			// (Ridgeness, Sphericalness, Cyclideness, Type)
19.8366 0.994136 147.776 1			//	* See the original paper of Yoshizawa for the definition
65.5137 0.973588 526.117 1			//	  of Ridgeness, Sphericalness, and Cyclideness
13.0411 0.929552 225.717 0			//	* Type: 0=Convex 1=Concave
77.8949 0.920558 2792.31 0
... ...
26 27 8556 0.734312 -0.510936 -0.446912		// list of segments: 
27 35 88480 0.735796 -0.513177 -0.441875	// (Ip1, Ip2, If, X-dir, Y-dir, Z-dir)
35 34 8577 0.733676 -0.517287 -0.440605		//	* Ip1 and Ip2 is the indices (to the list of points) of
34 30 8576 0.72921 -0.521361 -0.44321		//	  the two endpoints of the segment
30 29 8566 0.725694 -0.525892 -0.443627		//	* If is the facet the segment passing through
29 28 8565 0.72423 -0.529233 -0.442045		//	* -dir is the direction of this segment (this can be
28 31 8569 0.725229 -0.531389 -0.437798		//	  computed out of the point position, stored only for
31 32 8571 0.723684 -0.53345 -0.437851		//	  efficiency)
... ...

***************************************************************************************************************

Acknowledgement:
We would like to thank the providers of the following libraries/source codes:
CGAL (www.cgal.org/)
CHOLMOD (www.cise.ufl.edu/research/sparse/cholmod/)
Shin Yoshizawa's crest line extraction (www.riken.jp/brict/Yoshizawa/Research/Crest.html)
