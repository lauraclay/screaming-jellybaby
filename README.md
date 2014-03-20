# Make a Jelly Baby Scream!

You will learn how to turn a Jelly Baby into an input device for your Raspberry Pi. You will then create a program to make it scream when it is pressed.

##Requirements

- Raspberry Pi
- Micro USB power adaptor
- An SD card with Raspbian already set up through NOOBS
- USB keyboard
- USB mouse
- HDMI cable
- A monitor or TV
- Two metal paper clips or dress pins
- Two female to female jumper wires
- A Jelly Baby

## Step 0: Setting Up your Pi

First check that you have all the parts you need to get your Raspberry Pi set up and working.

- Raspberry Pi
- Micro USB power adaptor
- An SD card with Raspbian already set up through NOOBS
- USB keyboard
- USB mouse
- HDMI cable
- A monitor or TV

###Activity Checklist

1.	Place the SD card into the slot of your Raspberry Pi. It will only fit one way so be careful not to break the card. 
2.	Next connect the HDMI cable from the monitor (or TV) to the HDMI port on the Pi and turn on your monitor. 
3.	Plug the USB keyboard and mouse into the USB ports on the Pi.
4.	Plug in the micro USB power supply and you should see some text appear on your screen.
5.  When prompted to login type:

    ```
    Login: pi
    Password: raspberry
    ```

## Step 1: Wire up a Jelly Baby

To begin you will need to turn a simple jelly baby into a switch by attaching cables to it and then connecting them to the GPIO pins on a Raspberry Pi.


- Two metal paper clips or dress pins
- Two female to female jumper wires
- A Jelly Baby


### Activity Checklist

1. Take the metal paper clips and unfold them to make a straight wire.

2. Take a female to female jumper cable and push the paper clip wire into one of the ends. 

3. Do the same to the other wire so that you have two identical jumper cables with 

4. Insert the paper clips into a jelly baby so that they are close to each other but not touching. 

    Raspberry Pi GPIO header pins. The diagram above the pins shows the pin numbers. You will be using pin 3 and pin 25.

5. Take the other end of one of the jumper leads and push onto pin 3 of the General Purpose Input-Output (GPIO) header which is connected to one of the GPIO channels.

6. Take the end of the other jumper lead and push onto pin 25 of the GPIO header which is connected to ground.

    **Warning!** You can damage your Raspberry Pi if you do not use the GPIO pins correctly!

7. Set up the rest of your Raspberry Pi with an SD card with the latest Raspbian image installed via NOOBS, a keyboard, mouse, a HDMI cable to a monitor or TV, a connection to the internet, and a speaker so that you can hear your Jelly Baby screaming. [See the Raspberry Pi Quick Start Guide here](http://www.raspberrypi.org/quick-start-guide)    

8. Finally plug in a Micro USB power supply to start your Pi and log in. The default login for Raspberry Pi is: login `pi` and password `raspberry` 

9. If you are using headphones or a speaker on the Raspberry Pi you will need to run the following command to redirect sound to the headphone socket.

    `sudo amixer cset numid=3 1`

## Step 2: Downloading and playing screams!

So far you have created your input device and got your Raspberry Pi setup and running. You now need to download a scream sound file and install some software to be able to play it. This task can be achieved from the command line.

### Activity Checklist

1.  After logging into your Raspberry Pi you will see the following text:
    
    ```
    pi@raspberry ~ $
    ```
    The Raspberry Pi is waiting for you to type in a command to do something. This is referred to as the command line. 
    
2.  Download an mp3 sound effect to play when the Jelly Baby is pressed - all of this instruction should be typed on one line with the same uppercase and lowercase characters.

    ```
    wget http://goo.gl/MOXGX3 -O la.mp3 --no-check-certificate
    ```
    
3.  Now test that you can play the sound file using `omxplayer` by typing:

    ```
    omxplayer la.mp3
    ```
    
    ```omxplayer``` will play the downloaded sound file and you should hear it from the speaker or headphones connected to your Pi.
    
    If you cannot hear anything, make sure that your headphones or speakers are connected correctly.  If the jack/plug looks like the picture below (notice the **three** black bands) you may find that it will only work if you pull the plug out by a few milimeters.
    
    ![](./images/3-5mmjack.jpg "3.5 mm headphone jack")
    
## Step 3: Write a program in Python

The final step to make your Jelly Baby scream is to write a program in Python that detects when you press the Jelly Baby input device and outputs the scream sound.

### Activity Checklist

1. To write your Python program you will need to open a text editor window from the command-line. To do this type:

    ```
    nano scream.py
    ```

2. Begin your program by importing the modules and libraries needed to make it work. Type the following:

    ```python
    import time
    import RPi.GPIO as GPIO
    import os
    ```
    
    The time library will be used to make the program pause for a fixed amount of time. The Raspberry Pi GPIO libraries       will be used to connect the Raspberry Pi to other physical devices via the General Purpose Input-Output (GPIO) pins, in this case your Jelly Baby input device! The `os` library will be used to allow our program to call other programs that run on the Raspberry Pi like `omxplayer`.
    
3. Now you will need to set-up the General Purpose Input-Ouput (GPIO) pins to use GPIO board pin numbers. Leave a line empty by pressing enter on your keyboard, then type:

    ```python
    GPIO.setmode(GPIO.BOARD)
    ```
4. Now, to switch off warnings about "Ports already in use" press Enter to give you a new line and type:

    ```python
    GPIO.setwarnings(False)
    ```
5. Set pin 3 on the GPIO header to be an input

    ```python
    GPIO.setup(3,GPIO.IN)    
    ```
6. Create a loop that runs forever and plays the screaming sound file when the two wires inside the Jelly Baby are touching by typing:

    ```python
    while True:
        if GPIO.input(3) == False:
            os.system('omxplayer la.mp3')
            time.sleep(1);
    ```

7. Save the file by pressing `CTRL+X`, then `Y` for yes, followed by `Enter`.

8. Finally, run the program by typing:

    ```
    sudo python scream.py 
    ```
    
    **Congratulations!** Now when you press the Jelly Baby, the wires will touch and the mp3 file will play
    
9. Exit the program when finished by pressing `CTRL+C`

## Things to try:

- Using a real button or switch connected to a breadboard
- Changing the sound that plays when the device is pressed
- Can you think of a way to use more inputs?
    
