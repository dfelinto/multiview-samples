Multi View Samples
==================
Hosting the testing files and instructions for the multiview branch

Code branch in  git://git.blender.org/blender.git (multiview)

![BMW model by Mike Pan](http://wiki.blender.org/uploads/0/0d/Dev-Stereoscopy-MirroredSample.png "BMW model by Mike Pan")

This branch contains the code for the "stereoscopy support in Blender" journey.

Beta Builds
-----------
(outdated)
* [OSX](http://graphicall.org/1047) by [Francesco Siddi](http://twitter.com/fsiddi)
* [Linux](http://graphicall.org/1048) by [Alexey Akishin](https://github.com/Alexey-Akishin)
* [Windows 1](http://graphicall.org/1045)
* [Windows 2](http://builder.blender.org/download/) by [Blender Foundation](http://www.blender.org) / [BuildBot](http://buildbot.net)

Implemented Features
-----------
Render Views panel:

<img src="http://dalaifelinto.com/ftp/multiview/multiview_panel.jpg" alt="" width="235.5px" height="247.5px"/>

Switch View node:

<img src="http://dalaifelinto.com/ftp/multiview/multiview_switchview.jpg" alt="" width="161.5px" height="161px"/>

Image node (views options):

<img src="http://dalaifelinto.com/ftp/multiview/multiview_imagenode.jpg" alt="" width="150px" height="262px"/>

3-D display options (User Preferences > System):

<img src="http://dalaifelinto.com/ftp/multiview/multiview_stereodisplay.jpg" alt="" width="225.5px" height="253.5px"/>

3-D preview in Image Editor

<img src="http://dalaifelinto.com/ftp/multiview/multiview_stereo_imageeditor.jpg"/>

Current Status:
---------------
* See [Multiview Addon](https://github.com/dfelinto/multiview_addon) for the camera rig system
* [Youtube recording](http://www.youtube.com/watch?v=X7I6G3uRPkw&hd=1)
* **[Instructions for testing](https://github.com/dfelinto/blender/blob/multiview/HowToTestIt.md)**

**Known bugs:**
* (see the issues in the github tracker)
* Missing listeners - not everything is updating when they should if you change things after rendering

**Compositor elements not yet tackled:**
* Viewer Node

What do I plan to work next?
--------------------------------------

**Built-in Stereo Camera**:
If you read the original code proposal you should remember the original idea of having a builtin stereo-camera.
I didn't drop this idea, but there will be changes.

We will have a new stereo camera with all the nice properties (editable in 3D!).
Then you just assign this camera twice to two views in the Render View panel. The view panel can see the special camera and
give a menu where you can set left or right.

OR we will have addons for that ;)
UPDATE: I'm testing an addon and I think it may work well with it. So no builtin stereo camera for now.


Current issues
--------------------------
* Viewer Node showing only one view
* Sequencer not implemented

Links
-----
**Original proposal:** http://wiki.blender.org/index.php/User:Dfelinto/Stereoscopy

**Mailing list discussion:**
http://lists.blender.org/pipermail/bf-committers/2013-March/039601.html

**3d formats:**
http://news.cnet.com/8301-17938_105-20063310-1/how-3d-content-works-blu-ray-vs-broadcast/

**Active vs Passive:**
http://reviews.cnet.com/8301-33199_7-57437344-221/active-3d-vs-passive-3d-whats-better/

Roadmap
-------
 1. ~~Read multiview exr~~
 2. ~~See multiview in UV/image editor as mono~~
 3. ~~Write multiview exr~~
 4. ~~Render in multiview~~
 5. ~~Compo in multiview~~
 6. ~~See multiview in UV/image editor as stereo~~
 7. ~~Viewport preview~~
 8. Sequencer
 9. ?

How to build it
---------------
Note: Blender svn OpenEXR for windows may be buggy, they used to only work if you build a debug Blender.

For tips in building Blender for your system refer to the Blender Wiki:
* [Building Blender](http://wiki.blender.org/index.php/Dev:Doc/Building_Blender)
* [Git for Blender](http://wiki.blender.org/index.php/Dev:Doc/Tools/Git)


If you have a Blender building environment setup with arcanist, you can build with:
```
arc patch D43 # not updated at the moment, check the multiview branch in Blender 
```
I'll keep that [patch](http://developer.blender.org/D43) updated from time to time.
But you can always check the github repository with the following instructions.

Following instructions are for OSX with git 1.8.3.4. Don't use them literally try to make sense of them first.
```
mkdir multiview
cd multiview
git clone git://git.blender.org/blender.git --single-branch -b multiview blender
cd blender
git config submodule.scons.url git://git.blender.org/scons.git
git config submodule.release/scripts/addons_contrib.url git://git.blender.org/blender-addons-contrib.git
git config submodule.release/scripts/addons.url git://git.blender.org/blender-addons.git
git config submodule.release/datafiles/locale.url git://git.blender.org/blender-translations.git
git submodule update --init --recursive --remote
cd ..
ln -s ~/blender/lib lib; #HARDCODED folder to match my system
mkdir release
cd release
ccmake ../blender
make -j7 install
```

To update:
```
 cd multiview
 cd blender
 git pull --rebase
 git submodule update --recursive --remote
 cd ../release
 make -j7 install
 ```
