{% include mathjax_support.html %}
## Undergraduate final project (završni rad, senior thesis, honors thesis)

The written paper written by us in Croatian:
- [Google Drive](https://drive.google.com/file/d/1IeAkGCefQATIOI2VWCPJCTtHlTw8PiWc/view?usp=sharing)

Made during our study at Tehnička škola Slavonski Brod(Technical school Slavonski Brod) in the year 2022.

{%include youtubePlayer.html id='D6T-x6eK99k'%}

![rl model](/images/hexapod_rl_model.gif)

## 3D Model
The whole Hexapod was 3D printed in our school using the Ender 3. 
Made in CATIA V5.

All the CATIA part files and STL files are in the following link:
- [Google Drive](https://drive.google.com/drive/folders/1QQRWzVuSSnGnp3QAfDBRTR51gKrdCw-J?usp=sharing)

![animation](/images/walking.gif){:class="img-responsive" width="100%"}

### Body
![body](/images/body.png){:class="img-responsive" width="70%"}

### Joint 1
![joint 1](/images/joint1.png){:class="img-responsive" width="70%"} 

### Joint 2
![joint 2](/images/joint2.png){:class="img-responsive" width="70%"} 

### Joint 3
![joint 3](/images/joint3.png){:class="img-responsive" width="70%"} 

### Joint and Motor connection
![joint motor connection](/images/joint_motor_connection.png){:class="img-responsive" width="70%"} 

## Leg angle calculation
Derived from: 
- Agheli Hajiabadi, Mohammad Mahdi. Analytical Workspace, Kinematics, and Foot Force Based Stability of Hexapod Walking Robots. : Worcester Polytechnic Institute, 2013. 
[https://digital.wpi.edu/downloads/bk128b035](https://digital.wpi.edu/downloads/bk128b035)

### Vectors
$\vec S_{ix}$ - the constant distance from the center of the body of the Hexapod to the rotation point of the $x^{th}$ servo motor of the $i^{th}$ leg. 

$\vec l_{1i}$, $\vec l_{2i}$, $\vec l_{3i}$ - the length of joint 1, joint 2 and joint 3.

$\vec D$ - from the ground contact point to the center of the body of the Hexapod, given by the height and width of Hexapod gait.

$\vec l_i$ - from the ground contact point to the rotation point of the first servo motor.

$\vec {l'}_i$ - from the ground contact point to the rotation point of the second servo motor.

Adding an x, y or z to the vectors means we are taking the length of its projection on the given axis.

### Hip joint
To get the vector $\vec l_i$ we take the vector $\vec D$ and substract from it the vector $\vec s_{i1}$.

$$ \vec l_i = \vec D - \vec S_{i1} $$

To get the angle of the first servo motor we calculate the tangent of the projections of the vector $\vec l_i$ on the x and y axes.

$$ \alpha _i = \tan^{-1} \left( \frac{l_i x}{l_i y} \right)$$

### Knee joint
To get the vector $ \vec s_{i2}$ we add the vectors $\vec s_{i1}$ and $\vec l_{1i}$ with respect to the rotation of the first servo motor ($\alpha$), and the position of the leg based on the coordinate system ($(-1)^n$).

$$ \vec s_{i2} = \begin{bmatrix}
s_{i1x}+(-1)^n * l_{1i} * \cos \alpha _i\\ 
s_{i1y}+(-1)^n * l_{1i} * \sin \alpha _i\\
s_{i1z}
\end{bmatrix} $$

To get the vector $\vec {l'}_ i$ we take the vector $\vec D$ and substract from it the vector $\vec s_{i2}$.

$$ \vec {l'}_i = \vec D - \vec s_{i2}$$

### Knee and ankle angle

$$ \rho _i = \tan^{-1} \left( \frac {h'_i}{\sqrt {l'^2_{ix} + l'^2_{iy}}}\right)$$

$$ \varphi _i = \sin ^{-1} \left( \frac {h'_i - h_i}{l_{1i}} \right) $$

To get the angle $\beta _i$ we use a derivation of the cosine law and substract the angles $\rho _i$ and $\varphi _i$ to account for any rotation.

$$\beta _i = \cos ^{-1} \left( \frac {l_{i2}^2 + {l'}_i ^2 - l_{i3}^2 }{2 l_{i2} l_i} \right) - (\rho _i + \varphi _i)$$

To get the angle $\gamma _i$ we use a derivation of the cosine law and substract the angle from 180°($\pi$).

$$\gamma _i = \pi - \cos ^{-1} \left( \frac {l_{i2}^2 + l_{i3} ^2 - {l'}_i^2 }{2 l_{i2} l_{i3}}\right) $$

![vectors](/images/vector.png){:class="img-responsive"} 
![angles](/images/angle.png){:class="img-responsive" width="90%"} 

## Arduino code
Source code GitHub repository:
- [ArduinoHexapodControl](https://github.com/DorianK29/ArduinoHexapodControl)

## Android app code
GitHub repository:
- [HexapodApp](https://github.com/DorianK29/HexapodApp)

![Android app](/images/mobile_app.png){:class="img-responsive" width="30%"} 