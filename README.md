# Convert zhifengsoft (03eb:c8b4) USB ISP ASP AVR programmer to an USBasb programmer

---

You brought a cheap USB AVR that only can be used with ProgISP, which is not available for Linux or Mac? Here is a tutorial to compile USBasb to use the stick via avrdude, platformIO or Arduino IDE.

---

1. Have a look at this blog post https://www.sciencetronics.com/greenphotons/?p=938. __File in this repo has already been changed__. 

2. Add a wire to the self-programming jumper pins.

3. Connect the programmer to another programmer, for example an Arduino Uno that has the ISP sketch (File/Examples/11.ArduinoISP).

4. Install dependencies `apt-get install avrdude gcc-avr avr-libc`

5. Go into `firmware` sub directory and check the settings in `Makefile`. For example, some USB ISP use atmega8, others atmega88.

6. Compile: `make main.hex`

7. Set fuse: `avrdude -c avrisp -p atmega88 -b 19200 -P /dev/ttyACM1 -u -U hfuse:w:0xdd:m -U lfuse:w:0xff:m` or `make fuses`

8. Upload firmware: `avrdude -c avrisp -p atmega88 -P /dev/ttyACM1 -b 19200 -U flash:w:main.hex` or `make flash`

9. Remove jumper wire and enjoy. The USB ISP should now be recognised as USBasb device. 

