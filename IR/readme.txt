### Guide for setting Up LIRC on the RaspberryPi

Step 1 : Installation of LIRC Module on Raspberry PI 
	
sudo apt-get install lirc


Step 2 : Setup Lirc configuration to module file. 

Add following line to your /etc/modules file

lirc_dev
lirc_rpi gpio_in_pin=23 gpio_out_pin=22

Refer module file in the repository.

Step 3 : Modify /etc/lirc/hardware.conf and add lines as given in hardware.conf

Step 4 : Edit your /boot/config.txt file and add:
dtoverlay=lirc-rpi,gpio_in_pin=23,gpio_out_pin=22

 Refer boot/config.txt for details.


Step 5 : Reboot your RaspberryPi after making this change.

Testing the IR receiver

sudo /etc/init.d/lirc stop
mode2 -d /dev/lirc0

Point a remote control at your IR receiver and press some buttons. You should see something like this:

space 16300
pulse 95
space 28794
pulse 80
space 19395
pulse 83
space 402351


Testing the IR LED

# Stop lirc to free up /dev/lirc0
sudo /etc/init.d/lirc stop

# Create a new remote control configuration file (using /dev/lirc0) and save the output to ~/lircd.conf
irrecord -d /dev/lirc0 ~/lircd.conf

# Make a backup of the original lircd.conf file
sudo mv /etc/lirc/lircd.conf /etc/lirc/lircd_original.conf

# Copy over your new configuration file
sudo cp ~/lircd.conf /etc/lirc/lircd.conf

# Start up lirc again
sudo /etc/init.d/lirc start


irsend LIST samsung ""

sudo irsend SEND_ONCE samsung  KEY_POWER  --count=5#
