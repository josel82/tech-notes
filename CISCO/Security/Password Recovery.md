 In order to reset the passord you'll need to go into ROMMON mode, this can be achieve by sending a break signal during booting.

#### How to send break signal from a Macbook:

Open the terminal and run the following command:

$ screen /dev/tty.usbserial 1200

Start the cisco device

Press the space bar for about 30 seconds, you'll see some unreadable output on the terminal

After that, close that terminal session and open a new one.

This time run:

$ screen /dev/tty.usbserial 9600

Then press enter.

You should be in ROMMON mode

Follow the reset procedure

# Catalyst 2960

[https://www.cisco.com/c/en/us/support/docs/switches/catalyst-2950-series-switches/12040-pswdrec-2900xl.html](https://www.cisco.com/c/en/us/support/docs/switches/catalyst-2950-series-switches/12040-pswdrec-2900xl.html)

# Standard Procedure

[https://community.cisco.com/t5/networking-documents/password-recovery/ta-p/3123097](https://community.cisco.com/t5/networking-documents/password-recovery/ta-p/3123097)

# Tutorial
https://courses.davidbombal.com/courses/267624/lectures/4158971

