Malladi-Sethian Min-Max Noise Removal
==========================================================================================================================================
*This Matlab code uses Malladi and Sethian's Min-Max curvature based noise removal algorithm.*

This approach is based on level-sets (Osher-Sethian level set) and enhances the image by evolving the image under flow controlled by min/max curvature flow and by mean curvature. The basic idea is to solve a time-dependent partial differential equation that describes the evolution of isointensity contours using a switch function that assesses the scale of the noise and chooses the appropriate terms in the differential equations. It works well with both salt-and-pepper grey-scale noise and full-image continuous noise present in black and white images, grey-scale images, texture images and color images. The noise removal/enhancement schemes applied in this stage contains only one enhancement parameter, which in most cases is automatically chosen, and stop automatically at some optimal point. Continued application of the scheme produces no further change. 

Can also download from here: [![View psharma15/minmax-noise-removal on File Exchange](https://www.mathworks.com/matlabcentral/images/matlab-file-exchange.svg)](https://www.mathworks.com/matlabcentral/fileexchange/58927-psharma15-minmax-noise-removal)

## References:
1. [R. Malladi and J. A. Sethian, “Unified approach to noise removal, image enhancement, and shape recovery,” IEEE Trans. Image Processing, vol. 5, pp. 1554–1568, Nov. 1996.] (https://doi.org/10.1109/83.541425)
2. [S. Osher, R. Fedkiw, "Level set methods: An overview and some recent results", J. Comput. Phys., vol. 169, no. 2, pp. 463-502, 2001.] (https://doi.org/10.1006/jcph.2000.6636)
