Author: God Quest Bennett
====

Why: Setting up Cuda can be challenging. My guide helps setup Cuda from the example/scope of artificial car generation via generative adversarial network example.

This was offered in some of my blockchain offerrings like "these cars don't exist nft below" as well as of course, used to build that NFT, as well as components in other Cuda based products, like my Cryptosynth project's artificial images of people used as input to the 3d generator.
====

Side note: I created this process for help building out:
* [Cryptosyth product](https://github.com/g0dEngineer/Cryptosynth)
* [These car's don't exist NFT](https://www.instagram.com/p/CMLMvfbhHxE/)
* etc

The guide above was adapted from my older [ (2020) Deep Brain Seq Windows Installation Guide](https://github.com/JordanMicahBennett/DeepBrainSeg/blob/master/WINDOWS%2010%20INSTALLATION%20GUIDE.md).
====

Machine: i76700 cpu, 16 gb ram, 1 terabyte of storage, gtx 1060 6 gb

Requirements: Windows Desktop or laptop with at least GTX 1060 gpu.


Goal: This particular instruction will help the setup of a Gan based car clip generator.

![image](https://github.com/g0dEngineer/CUDA_STYLEGAN_SETUP_GUIDE/blob/main/mega%20cuda%20setup%20guide__.png)

1. Download and install python 3.6.

2. Download stylegan 2 python project: -> https://github.com/justinpinkney/stylegan2

3. Update graphics drivers. (Any applicable nvidia gpu driver)

4. Install Cuda 10.

5. Download cuDNN v7.5  for CUDA 10.0.

6. Install visual studio 2017 commnunity.

7. Install visual studio 14 if not already installed. Something like "C:\Program Files (x86)\Microsoft Visual Studio 14.0" should exist after install.

8. After doing 2017 commnunity run install again, and modify 2017 commnunity to include (a few gigs):
	i. Windows Universal CRT SDK
	ii. Windows 10 SDK 
	iii. VC++ 2015.3 v14.00 toolset for tesktop

9. Ensure environement variable is setup to include items similar to the following:
	C:\Users\18765\AppData\Local\Programs\Python\Python36
	C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\bin
	C:\Program Files (x86)\Windows Kits\10\Include\10.0.10240.0\ucrt
	C:\Users\18765\Downloads\cudnn-10.0-windows10-x64-v7.5.0.56\cuda\bin
	C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0\bin
	C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0\libnvvp

10. Modify lib/include in environment variables:
	INCLUDE:
	C:\Program Files (x86)\Windows Kits\10\Lib\10.0.10240.0\ucrt

	LIB
	C:\Program Files (x86)\Windows Kits\10\Lib\10.0.10240.0\um\x64
	C:\Program Files (x86)\Windows Kits\10\Lib\10.0.10240.0\ucrt\x64
		
		
11. Install tensorflow-gpu 1.14.0.
	Note if you get dlib build red line errors, you need to:
		Install cmake 3.19.4, and visual studio build tools. (this build tools is different from the items prior)
		After installing build tools.
	
12. Ensure tensorflow is not installed. Ensure only tensorflow-gpu 1.14.0 is installed.

13. Restart computer. Tensorflow may not detect GPU until restart.

14. Navigate to cuda 10 bin. Right click on cudafe++.exe, and enable run as administrator , to avoid "nvcc error : 'cudafe++' died with status 0xC0000005 (ACCESS_VIOLATION)" error. God Bennett (myself) came up with this quick solution, instead of the CUDA 10.1 download workaround solution proposed online, which is 2 gb download.
	Example location: C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0\bin

	
15. Download at least 1 car stylegan model from https://drive.google.com/drive/folders/1yanUI9m4b4PWzR0eurKNq6JR1Bbfbh6L. 
This is the same as models provided by NVIDIA/stylegan2. Can be any one from "stylegan2-car-config-a.pkl" to "stylegan2-car-config-f.pkl".


16. We will not use the the grid_vid.py latent walk generator from justinpinkney/stylegan2, which leads to an Operand error at execution on the pretrained model.


a) Instead, download lzhbrian's copy of "gen_video_interpolation.py" from https://gist.github.com/lzhbrian/75dd7e58444c4469b4b341d36b0cc09b#file-gen_video_interpolation-py.

b) Make the necessary changes, to load any of the "stylegan2-car...pkl" networks, by changing fpath variable.

Example fpath = 'C:/Backup/Downloads/God/RobotizeJA/crypto/ai_generated_cars/stylegan2-master_pin/stylegan2-car-config-f.pkl'

c) Make sure to specify output file name, where resulting video will be stored, by modifying mp4 parameter in generate_interpolation_video function.

Example  mp4='C:/Backup/Downloads/God/RobotizeJA/crypto/ai_generated_cars/stylegan2-master_pin/output.mp4'

d) You can also modify other parameters there, like video duration.

17. Get ffmpeg in python idle:
	import imageio
	imageio.plugins.ffmpeg.download()
 
 
18. Run interpolation python script: Example -> python C:/Backup/Downloads/God/RobotizeJA/crypto/ai_generated_cars/stylegan2-master_pin/gen_video_interpolation.py
