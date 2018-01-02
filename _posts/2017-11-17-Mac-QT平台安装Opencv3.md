---
layout:   post
title:    "Mac QT平台安装Opencv3"
subtitle: "Opencv"
date:     2017-11-17
author:   "NL"
header-img: "img/post-bg-2015.jpg"
tags:
    - Opencv	
---

[转载](http://www.jianshu.com/p/5565ba6c793b).

## 开始

1) 从官网下载并安装QT5.7.0 opensource离线安装版
官网地址：<https://www.qt.io/download-open-source/#section-2>
安装后就能在安装目录里找到QtCreator了

2) 通过brew安装opencv3

```
brew install opencv3 --with-contrib --with-ffmpeg --with-gphoto2 --with-gstreamer --with-jasper --with-java --with-opengl --HEAD
```

说明：

```
--32-bit
    Build 32-bit only
--c++11
    Build using C++11 mode
--universal
    Build a universal binary
--with-cuda
    Build with cuda support
--with-ffmpeg
    Build with ffmpeg support
--with-gstreamer
    Build with gstreamer support
--with-jasper
    Build with jasper support
--with-java
    Build with Java support
--with-libdc1394
    Build with libdc1394 support
--with-opengl
    Build with OpenGL support
--with-openni
    Build with openni support
--with-qt
    Build the Qt4 backend to HighGUI
--with-quicktime
    Use QuickTime for Video I/O instead of QTKit
--with-tbb
    Enable parallel code in OpenCV using Intel TBB
--with-vtk
    Build with vtk support
--with-ximea
    Build with XIMEA support
--without-eigen
    Build without eigen support
--without-numpy
    Use a numpy you've installed yourself instead of a Homebrew-packaged numpy
--without-opencl
    Disable GPU code in OpenCV using OpenCL
--without-openexr
    Build without openexr support
--without-python
    Build without Python support
--without-test
    Build without accuracy & performance tests
--HEAD
    Install HEAD version
```

3) 找到opencv链接库

设置下PKG_CONFIG_PATH环境
`export PKG_CONFIG_PATH=${PKG_CONFIG_PATH}:/usr/local/opt/opencv3/lib/pkgconfig`

通过 `pkg-config --libs opencv` 命令获取lib位置
如：

```
$ pkg-config --libs opencv
-L/usr/local/Cellar/opencv3/HEAD/lib -lopencv_stitching -lopencv_superres -lopencv_videostab -lopencv_aruco -lopencv_bgsegm -lopencv_bioinspired -lopencv_ccalib -lopencv_cvv -lopencv_dnn -lopencv_dpm -lopencv_fuzzy -lopencv_line_descriptor -lopencv_optflow -lopencv_plot -lopencv_reg -lopencv_saliency -lopencv_stereo -lopencv_structured_light -lopencv_rgbd -lopencv_surface_matching -lopencv_tracking -lopencv_datasets -lopencv_text -lopencv_face -lopencv_xfeatures2d -lopencv_shape -lopencv_video -lopencv_ximgproc -lopencv_calib3d -lopencv_features2d -lopencv_flann -lopencv_xobjdetect -lopencv_objdetect -lopencv_ml -lopencv_xphoto -lopencv_highgui -lopencv_videoio -lopencv_imgcodecs -lopencv_photo -lopencv_imgproc -lopencv_core
```

## 测试下

新建QT项目，设置include和libs

```
macx{
 INCLUDEPATH += /usr/local/opt/opencv3/include
 LIBS += -L/usr/local/Cellar/opencv3/HEAD/lib -lopencv_stitching -lopencv_superres -lopencv_videostab -lopencv_aruco -lopencv_bgsegm -lopencv_bioinspired -lopencv_ccalib -lopencv_cvv -lopencv_dnn -lopencv_dpm -lopencv_fuzzy -lopencv_line_descriptor -lopencv_optflow -lopencv_plot -lopencv_reg -lopencv_saliency -lopencv_stereo -lopencv_structured_light -lopencv_rgbd -lopencv_surface_matching -lopencv_tracking -lopencv_datasets -lopencv_text -lopencv_face -lopencv_xfeatures2d -lopencv_shape -lopencv_video -lopencv_ximgproc -lopencv_calib3d -lopencv_features2d -lopencv_flann -lopencv_xobjdetect -lopencv_objdetect -lopencv_ml -lopencv_xphoto -lopencv_highgui -lopencv_videoio -lopencv_imgcodecs -lopencv_photo -lopencv_imgproc -lopencv_core
}
```

测试代码：

```
#include <iostream>
#include "opencv2/opencv.hpp"

using namespace std;

int main(int argc, char *argv[])
{
 cv::Mat img = cv::imread("/Users/vell/Pictures/desktop.jpg");
 cv::imshow("Image", img);
 cv::waitKey(0);

 return 0;
}
```