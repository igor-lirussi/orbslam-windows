# ORB_SLAM2_Windows
Easy build for ORB Slam 2 on Windows

1. Make a directory called build in orbslam-windows/Thirdparty/DBoW2
- Run CMake GUI and set source code to orbslam-windows/Thirdparty/DBoW2 and where to build the binaries to orbslam-windows/Thirdparty/DBoW2/build
- Press Configure and choose Visual Studio 14 2015 Win64 or Visual Studio 12 2013 Win64
- Press Generate
- Open the resulting project in the build directory in Visual Studio
- Change build type to Release (in white box up top, should initially say Debug)
- Right click on DBoW2 project -> Properties -> General: change Target Extension to .lib and Configuration Type to Static Library (.lib)
- Go to C/C++ Tab -> Code Generation and change Runtime Library to Multi-threaded (/MT)
- Build ALL_BUILD. You should get lots of warnings but no errors

2. Make a directory called build in orbslam-windows/Thirdparty/g2o
- Run CMake GUI and set source code to orbslam-windows/Thirdparty/g2o and where to build the binaries to orbslam-windows/Thirdparty/g2o/build
- Press Configure and choose Visual Studio 14 2015 Win64 or Visual Studio 12 2013 Win64
- Press Generate
- Open the resulting project in the build directory in Visual Studio
- Change build type to Release (in white box up top, should initially say Debug)
- Right click on g2o project -> Properties -> General: change Target Extension to .lib and Configuration Type to Static Library (.lib)
- Go to C/C++ Tab -> Code Generation and change Runtime Library to Multi-threaded (/MT)
- Go to C/C++ -> Preprocessor and press the dropdown arrow in the Preprocessor Definitions, then add a new line with WINDOWS on it (no underscore), then press OK, then Apply
- Build ALL_BUILD.

3. Make a directory called build in orbslam-windows/Thirdparty/Pangolin
- Run CMake GUI and set source code to orbslam-windows/Thirdparty/Pangolin and where to build the binaries to orbslam-windows/Thirdparty/Pangolin/build
- Press Configure and choose Visual Studio 14 2015 Win64 or Visual Studio 12 2013 Win64. You'll have a lot of RED and a lot of things that say DIR-NOTFOUND but as long as the window at the bottom says Configuring Done you're fine
- Press Generate
- Open the resulting project in the build directory in Visual Studio
- Change build type to Release (in white box up top, should initially say Debug)
- Build ALL_BUILD. You'll have an error by project testlog that says "cannot open input file 'pthread.lib'" but that doesn't matter cause we don't use testlog. Everything else should build fine, i.e., you should have
========== Build: 18 succeeded, 1 failed, 0 up-to-date, 0 skipped ==========

3. Make a directory called build in orbslam-windows
- Run CMake GUI and set source code to orbslam-windows and where to build the binaries to orbslam-windows/build
- Press Configure and choose Visual Studio 14 2015 Win64 or Visual Studio 12 2013 Win64
- Press Generate
- Open the resulting project in the build directory in Visual Studio
- Change build type to Release (in white box up top, should initially say Debug)
- Right click on ORB_SLAM2 project -> Properties -> General: change Target Extension to .lib and Configuration Type to Static Library (.lib)
- Go to C/C++ Tab -> Code Generation and change Runtime Library to Multi-threaded (/MT)

I had to disable warnings in Orb Slam because otherwise there were so many they crashed visual studio. You will still see a few but not very many

- Right click on the ORB_SLAM2 project (NOT ALL_BUILD) and click Build
- If you're lucky, that will take few minutes then successfully build!

If you want to build any of the examples (such as mono_euroc), do the following:

- Right click on that project and go to Properties -> C/C++ -> Code Generation, and change Runtime Library to Multi-threaded (/MT). Then press apply
- Right click on it and press build

Then you will find them, say if you do mono_, in (orbslam-windows\Examples\Monocular\Release)


### HOW TO EXECUTE
a.k.a. my commands collection

inside folder "orbslam-windows" with command line (I used GIT BASH)

NOTE: change "sequenze_prova" folder with your folder containing the datasets
#### MONOCULAR
- ###### EuRoC V1
Download a sequence (ASL format) from http://projects.asl.ethz.ch/datasets/doku.php?id=kmavvisualinertialdatasets
```
./Examples/Monocular/Release/mono_euroc Vocabulary/ORBvoc.txt Examples/Monocular/EuRoC.yaml sequenze_prova/EuRoC/V1_01_easy/mav0/cam0/data Examples/Monocular/EuRoC_TimeStamps/V101.txt
```

- ###### EuRoC MH1
Download the dataset like before
```
./Examples/Monocular/Release/mono_euroc Vocabulary/ORBvoc.txt Examples/Monocular/EuRoC.yaml sequenze_prova/EuRoC/MH_01/cam0/data Examples/Monocular/EuRoC_TimeStamps/MH01.txt
```

- ###### TUM freiburg 1
Download a sequence from http://vision.in.tum.de/data/datasets/rgbd-dataset/download and uncompress it.
```
./Examples/Monocular/Release/mono_tum Vocabulary/ORBvoc.txt Examples/Monocular/TUM1.yaml sequenze_prova/TUM/rgbd_dataset_freiburg1_desk
```

- ###### KITTI
Download the dataset (grayscale images) from http://www.cvlibs.net/datasets/kitti/eval_odometry.php
```
./Examples/Monocular/Release/mono_kitti Vocabulary/ORBvoc.txt Examples/Monocular/KITTI04-12.yaml sequenze_prova/KITTI/13
```

#### RGB-D
##### You need to associate RGB and Depth with Python (I used Pyhton 2):
```
python associate.py sequenze_prova/TUM/rgbd_dataset_freiburg1_desk/rgb.txt sequenze_prova/TUM/rgbd_dataset_freiburg1_desk/depth.txt > associations.txt
```
##### Then from command line:
- TUM freiburg 1 associations created:
```
./Examples/RGB-D/Release/rgbd_tum Vocabulary/ORBvoc.txt Examples/RGB-D/TUM1.yaml sequenze_prova/TUM/rgbd_dataset_freiburg1_desk associations.txt
```

- TUM freiburg 1 associations default:
```
./Examples/RGB-D/Release/rgbd_tum Vocabulary/ORBvoc.txt Examples/RGB-D/TUM1.yaml sequenze_prova/TUM/rgbd_dataset_freiburg1_desk Examples/RGB-D/associations/fr1_desk.txt
```

#### STEREO
- ###### EuroC V1
```
./Examples/Stereo/Release/stereo_euroc Vocabulary/ORBvoc.txt Examples/Stereo/EuRoC.yaml sequenze_prova/EuRoC/V1_01_easy/mav0/cam0/data sequenze_prova/EuRoC/V1_01_easy/mav0/cam1/data Examples/Stereo/EuRoC_TimeStamps/V101.txt
```

- ###### EuroC MH1
```
./Examples/Stereo/Release/stereo_euroc Vocabulary/ORBvoc.txt Examples/Stereo/EuRoC.yaml sequenze_prova/EuRoC/MH_01/cam0/data sequenze_prova/EuRoC/MH_01/cam1/data Examples/Stereo/EuRoC_TimeStamps/MH01.txt
```

- ###### KITTI
```
./Examples/Stereo/Release/stereo_kitti Vocabulary/ORBvoc.txt Examples/Stereo/KITTI04-12.yaml sequenze_prova/KITTI/13
```

#### WEBCAM
```
./Examples/Monocular/Release/mono_webcam Vocabulary/ORBvoc.txt Examples/Monocular/webcam.yaml
```

#### HTTP STREAM
```
./Examples/Monocular/Release/mono_http_igor Vocabulary/ORBvoc.txt Examples/Monocular/webcamMIA.yaml http://10.1.20.140:8080
```

#### VIDEO ( video goes inside orblasm-windows-http)
```
./Examples/Monocular/Release/mono_http_igor Vocabulary/ORBvoc.txt Examples/Monocular/webcamMIA.yaml ./video.mp4
```
#### Video from smartphone
```
./Examples/Monocular/Release/mono_http_igor Vocabulary/ORBvoc.txt Examples/Monocular/smartphoneMIO.yaml ./videosmartphone.mp4
```
