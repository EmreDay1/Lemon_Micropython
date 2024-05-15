# Lemon_Micropython
This is the library for controlling Lemon Robots with micropython via the RaspberryPi Pico, It is a library which acsess the PCA9685 servo controller, it was built due to the adafruit PCA9685 library being deprecated


Firstly, you must connect your Pico to your computer with the pico cable. Then you must connect the PCA9685 to your Pico. Firstly you must connect the SCL, SDA, VCC and Ground pins of the PCA9685 to your picos General Purpose Input Output(GPIO) pins. You should connect SDA to pin zero, SCL to pin one.![073cf75b-f7a1-41f8-8be5-8a3ceca66a8d](https://github.com/HisarCS/Lemon_Micropython/assets/120194760/a306004c-99e0-4492-924a-61f84acff67c) Then you should connect VCC to pin 40 and Ground to pin 38 as seen in the image below. <img width="659" alt="Ekran Resmi 2023-07-14 22 05 38" src="https://github.com/HisarCS/Lemon_Micropython/assets/66021457/c94857f9-6346-425e-9317-646f2ec98a96">

Then you must connect a power source(preferably 4.5-5V) to the power pins located on the side of the PCA9685 because the pico only powers the logic gates of the PCA9685.In this case we are using a 9V power supply so to regulate it to 5 volts we will use a 5v regulator.
![b37e0d73-a2cf-4f8c-b466-8e863f9dd265](https://github.com/HisarCS/Lemon_Micropython/assets/120194760/3c28182c-8ede-4216-95c7-40cf21b59ac7)

Lastly, you must connect servos to the PCA9685. Whilst connecting the servo the orange female pin will be connected to PWM male pin, the red female pin will be connected to the V+ male pin and the black female pin will be connected to the GND male pin.<img width="620" alt="Ekran Resmi 2023-07-17 14 28 12" src="https://github.com/HisarCS/Lemon_Micropython/assets/66021457/58ca47c6-1f85-48f8-8a59-d0422ac80a80">



Secondly, you must prepare the LemonLib library to perform the necessary functions needed to control your robot. First, you must create a folder named Lemon then you must open your computer’s terminal and write cd Lemon. Then, you must write git clone (library link). After completing this process you will have installed the library. Next, you must install the IDE Mu Editor. (Mu editor için gereken adımları ekle). 

This library works for the Lime and Satsuma robots. To control your Lime robot, you must perform the following steps. Firstly, you must import the Lemon library with the following line :

```python

import LemonLib

```

Then you must initialize your I2C 
channel:

```python
i2c = I2C(0, scl=Pin(1), sda=Pin(0))
```

The following function from the I2C class in the machine library takes three arguments. The second and the third one initialize the set pins for the I2C channel. And the first argument sets which I2C channel the PCA9685 is. After that, you must set the I2C channel you have just created for your PCA9685 and also set your PWM frequency.
```python
pca = PCA9685(i2c)
pca.set_pwm_freq(50)
```
Then you must create a while loop in order to move the fish.
```python
while True:
      for angle in range:(0, 180, 5):
          pca.set_angle(0, angle)
          pca.set_angle(1, angle)
          print(angle)
          time.sleep(0.05)

     for angle in range(180, 0, -5):
          pca.set_angle(0, angle)
          pca.set_angle(1, angle)
          print(angle)
          time.sleep(0.05)
```

The angle in range functions make the Lime fish move from 0 to 180 and then from 180 to 0 5 degrees at a time. Whilst the pca.set_angle function sets the current angle value created in the loops to the servos on the PCA9685’s first and second channels, the print(angle) function shows you the current angle value which is created by the for loops. Also the time.sleep(0.05) smooths out the movement of the fish by creating a small time interval between each iteration of the loop.

Secondly, to control the Satsuma robot.
To control your Satsuma robot, you must perform the following steps. Firstly, you must import the Lemon library with the following line :

```python

import LemonLib

```

Then you must initialize your I2C 
channel:

```python
i2c = I2C(0, scl=Pin(1), sda=Pin(0))
```

The following function from the I2C class in the machine library takes three arguments. The second and the third one initialize the set pins for the I2C channel. And the first argument sets which I2C channel the PCA9685 is. After that, you must set the I2C channel you have just created for your PCA9685 and also set your PWM frequency.
```python
pca = PCA9685(i2c)
pca.set_pwm_freq(50)
```

```python
while True:
        pca.set_angle(0, 40)
        pca.set_angle(1, 90)
        pca.set_angle(2, 40)
        pca.set_angle(3, 50)
        pca.set_angle(4, 90)

        time.sleep(0.5)

        pca.set_angle(0, 20)
        pca.set_angle(1, 110)
        pca.set_angle(2, 20)
        pca.set_angle(3, 90)
        pca.set_angle(4, 50)
```
This creates the loop for the turtle to go between the set intervals for it to move according to the initial design


