# Mac Troubleshooting

## Safe Mode
Starting your Mac in safe mode is useful when you're trying to resolve an issue that doesn't seem to be related to using any particular app. 

To start your Mac in Safe Mode:

1. Turn on or restart your Mac, and immediately press and hold the Shift key as your Mac starts up.
2. Release the Shift key when you see the login window. ”Safe Boot” should appear in the upper-right corner.
3. Log in to your Mac. 

## SMC Reset
The SMC on your Mac is responsible for managing the following features:

* Power, including the power button and power to the USB ports
* Battery and charging
* Fans and other thermal-management features
* Indicators or sensors such as status lights (sleep status, battery charging status, and others), the sudden motion sensor, the ambient light sensor, and keyboard backlighting
* Issues when opening and closing the lid of a notebook computer

If you're experiencing issues with any of the above features, you might need to reset the SMC. 

### To reset the SMC on your Mac:

1. Shut down your Mac.
2. On your built-in keyboard, press and hold all of the following keys. Your Mac might turn on.
3. Control  on the left side of your keyboard
4. Option (Alt)  on the left side of your keyboard
5. Shift  on the right side of your keyboard
6. Keep holding all three keys for 7 seconds, then press and hold the power button as well. If your Mac is on, it will turn off as you hold the keys.
7. Keep holding all four keys for another 7 seconds, then release them.
8 .Wait a few seconds, then press the power button to turn on your Mac.

## PRAM/NVRAM Reset
Settings that are stored in PRAM/NVRAM on your Mac include:

* Sound volume
* Display resolution
* Startup-disk selection
* Time zone
* Recent kernel panic information
* If your Mac has issues related to settings listed above, resetting the PRAM/NVRAM might help.

### To reset the PRAM/NVRAM on your Mac:

1. Shut down your Mac,
2. Turn it on and immediately press and hold these four keys together: 
3. Option, Command, P, and R.
4. Release the keys after about 20 seconds, during which your Mac might appear to restart.

## Verbose Mode
For troubleshooting software or third party apps, this mode will let you see line by line the output as it boots up. This is good for the following:

* Developers having issues with apps
* Having startup issues where the Mac is crashing and causing a kernel panic
* Seeing if support software has loaded for peripherals
* To boot into verbose mode, do the following:

1. Shut down your Mac
2. Turn it on and immediately press and hold these two keys together: 
  Command, V

You will know you are in verbose mode when white text appears on the screen and you will exit automatically when it progresses sufficiently.

## Apple Diagnostics

To test the hardware of your Mac, you can choose to boot into Apples diagnostics tool doing the following.

1. Shut down your Mac
2. Turn it on and immediately press and hold the D key
3. Release the D key when the prompt appears asking you to choose your language
Your Mac will run a diagnostic test for about five minutes and provide the results
