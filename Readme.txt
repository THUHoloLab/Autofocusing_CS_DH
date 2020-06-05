Refer to Instruction.doc.


Autofocusing_compressive_holography_twin_image_removal

1. Introduction
Autofocusing_compressive_holography_twin_image_removal is a tool that can achieve some functions. It can generate holograms that produced by a specimen (USAF_simulation) under plane incident light and reconstruct the hologram by autofocusing method and perform twin image removal. 

2 System Requirements
 
* Matlab R2016a or newer, earlier versions should also work but not tested.
 

3 Usage
Run the example codes which are named ‘main.m’.
Example picture is named ‘USAF_simulation.tif’.


4.1 Generate holograms (Gabor in-line holography)
See the example 'main.m' as following:
Input a picture 'USAF_simulation.tif' to generate a hologram which is located at z µm above the sensor plane. 
 
Matlab
%% Parameters (1)
o = imread('USAF_simulation.tif');
o = rgb2gray(o);
o = imresize(o,[500,500]);
o = im2double(o);
f=o;
figure;imshow(abs(f));title('Object') % show the object

nx=size(f,1);  
ny=size(f,2);
nz=1;
lambda=0.532;  % wavelength (um)
k = 2*pi/lambda;
detector_size=3.75;  % pixel pitch (um)
sensor_size=nx*detector_size;  % detector size (um)
z=1550;  % distance from object plane to detector plane (um)
deltaX=detector_size;
deltaY=detector_size;
Nx=nx;
Ny=ny*nz*2;
Nz=1;
You can use other parameters to change the properties of incident light, sensor plane and distance of object to recording plane. 

4.2 Reconstruct the hologram and perform twin image removal
Now the recorded hologram is input to reconstruct (maybe you can input your own hologram).
The ‘LAP’ is the autofocusing metric to estimate the focal plane during the reconstruction. You can get the results of focal plane estimate in MappedData1. 
When you obtain the appropriate reconstruction distance through ‘LAP’, the 'TwIST' are used to eliminate the twin image in reconstructed image.
 
To use these functions, you need to set parameters.
See the example 'main.m' below :
Matlab
%% Parameters (4)
z_start=1290; %start hologram plane to reconstruction plane distance in um
z_end=1800;  %end hologram plane to reconstruction plane distance in um
z_step=10; % step hologram plane to reconstruction plane distance in um

%% TwIST algorithm (8)
tau=0.04; % regularization parameter, usually a non-negative real parameter of the objective function
piter = 4; % one of the parameters of TV denoise
tolA = 1e-6; % the cut-off conditions of algorithm
iterations =250; % number of iterations
You can use other parameters  to adjust range of reconstruction distance and the function of TwIST.

If you want to learn more about compressive holography, you can refer to the paper at ‘Reference’.





5 References
1. Brady D J, Choi K, Marks D L, Horisaki R and Lim S. "Compressive Holography." Opt. Express     
17, 13040-13049 (2009).
2. Hua Zhang, Liangcai Cao, Hao Zhang, Wenhui Zhang, Guofan Jin. "Noise reduction for  
compressive digital one-shot in-line holographic tomography." HolographyVII, Vol.10022, p.1002207, SPIE, Photonic Asia (2016).
3. Hua Zhang, Liangcai Cao, Hao Zhang, Wenhui Zhang, Guofan Jin, and David J. Brady, "Efficient
 block-wise algorithm for compressive holography." Opt. Express 25, 24991-25003 (2017).
4. Wenhui Zhang, Liangcai Cao, David J. Brady, Hua Zhang, Ji Cang, Hao Zhang, and Guofan Jin,
 "Twin-Image-Free Holography: A Compressive Sensing Approach." Phys. Rev. Lett. 121, 093902
(2018).




                                                             
Update: 2020. 06. 05
Editor: Yiyi Zhang
Laboratory leader: Liangcai Cao

