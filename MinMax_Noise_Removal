function MinMax_Noise_Removal(input_img, R, Th, dt)

%% This code uses Malladi and Sethian Min-Max Noise Reduction method  
% This works on grayscale images in double form 
% input_img: input image can be in any format. Needs to be a square matrix.
% R: Radius of disk over which average of phi will be taken  to decide Min/ 
% Max speed function
% Th: Threshold to compare Avg (phi over disk of R) 
% dt: Step of Upwind Finite Difference Method
% Example to use is: MinMax_Noise_removal('test.jpg',5,0.8,0.01)
% -------------------------------------------------------------------------
% Pragya Sharma, Cornell University, 07-21-2016
% -------------------------------------------------------------------------

%% Code starts here

% Resizing image and converting to double square matrix format
img_orig=im2double(imresize(rgb2gray(input_img),[100,100]));
img=padarray(img_orig,[R,R],'replicate','both');

phi = img;
[m,n]= size(phi);

% F is the Min/Max speed function. Preallocation done here.
F = zeros(m,n);
D_negx=zeros(m,n);
D_posx=zeros(m,n);
D_negy=zeros(m,n);
D_posy=zeros(m,n);

% Time for iterations. Note the image would not change anymore if t0 is
% sufficiently high
t0 = 500;

for t=1:t0
    [phi_x,phi_y]=gradient(phi);
    s=sqrt(phi_x.^2 + phi_y.^2);
    smallNumber=1e-10;  
    % Adding a small positive number to avoid division by zero
    Nx=phi_x./(s+smallNumber); 
    Ny=phi_y./(s+smallNumber);
    [nxx,~]=gradient(Nx);  
    [~,nyy]=gradient(Ny);
    % Originally Malladi and Sethian took negative signed distance function
    % in the interion of the object, thus the sign of curvature
    K_dash=(nxx+nyy);
    K=-K_dash;
    
    for i = R+1:m-R
        for j=R+1:n-R
            avg=mean2(phi(i-R:i+R,j-R:j+R));
            % The following condition is opposite to the original paper
            if avg < Th;
               % Diffuses away all the information
                F(i,j)=max(K(i,j),0);
            else
                % Preserves some of the structure of the curve
               F(i,j)= min(K(i,j),0); 

            end
            
            % Solving the PDE with Upwind Method: forward and backward 
            % differences with h=1
            D_negx(i,j)=phi(i,j)-phi(i-1,j);
            D_posx(i,j)=phi(i+1,j)-phi(i,j);
            D_negy(i,j)=phi(i,j)-phi(i,j-1);
            D_posy(i,j)=phi(i,j+1)-phi(i,j);
            phi(i,j)=phi(i,j)-F(i,j)*dt*(max(D_negx(i,j),0)^2 + ...
                min(D_posx(i,j),0)^2 + max(D_negy(i,j),0)^2 + ...
                min(D_posy(i,j),0)^2)^0.5;
                        
        end
    end
end

It=phi(R+1:m-R,R+1:n-R);
i=(abs(It));

figure;
p1 = subplot(1,2,1);
set(gcf,'renderer','painters');
mesh(img_orig); colormap gray; axis 'equal'; view(0,90)
title 'Original Image'

p2 = subplot(1,2,2);
set(gcf,'renderer','painters');
mesh(i); colormap gray; axis 'equal'; view(0,90)
title 'Noise Removed Image'

linkaxes([p1,p2],'xy')
