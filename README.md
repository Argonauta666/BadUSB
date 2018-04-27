# BadUSB

![BadUSB](/baduino.jpg)


Baduino is a device by which HID devices can be imitated and commands can be sent to the corresponding Operating System. A pre-prepared script reads and runs the script files from the storage device attached to the storage module.

<b>quipment</b>

![Baduino](http://i.imgur.com/mnQKtk9.png)

The circuit elements shown above with the connections shown above;

SparkFun Pro Micro 5V/16Mhz ya da 3.3V/8Mhz
MicroSD Card Module
DIP Switch(4'lü)

Since the card uses the SPI communication standard with the MicroSD module, we can not use the USB Host Conroller feature, which means that we do not have the option of exchanging files with the target Operating System.

We use the DIP Switch to select previously prepared scripts.

<b>Software</b>

<b>Part 1 - Interpreter</b>

commands

REM - Comment line, characters on this line are ignored by the interpreter.

STRING - Text input, the characters in this line are sent by the interpreter to the Operating System as a "key press event". For example, we have a command like "STRING Hello World". When the text document is clearly attached to the computer Baduino writes "Hello World" to the text document. Prints text in any text entry field.

DELAY - Baduino is as fast as your computer. For example, if you are downloading a 10MB file from FTP, you can not expect it to take a minute or so. You need to add delay as much as possible to such situations, and as short as possible for privacy. If you add an insufficient delay time, the expected operation and subsequent operations will not be performed properly.

Except for the 3 basic commands above,

CTRL SHIFT CAPS ENTER BACKSPACE SPACE F1-12 ESC . . .

Keys are often used in script files. For example, to open the search bar screen, the "GUI" command that activates the Windows Logon key is written. This is how the start menu opens. A program called in this section, for example "cmd", is run with administrator rights as follows.

DELAY 3000 GUI DELAY 1000 STRING cmd DELAY 500 CTRL SHIFT ENTER DELAY 1000 ALT y

The GUI opens the Start Menu via command. STRING is cmd and it says "cmd". CTRL SHIFT Pressing ENTER opens the dialog window to run as Administrator. In the Dialog Window opened with ALT y, we give "Yes" confirmation.

The results you get when trying to enter these commands yourself are the same. Baduino scripts attack the system by mimicking a completely physical keyboard. We should not neglect to add delays and this is where you should pay attention.

<b>Part 2 - Things to Watch Out For</b>

Certain Turkish characters (ğüçöşı, ĞUŞİÇÖ) should not be used in directory names. There is no objection to comment lines. Briefly, Turkish characters should not be used in all lines considered by the Interpreter.

Arduino IDE will reinstall the Arduino IDE when new software is being added, after this address is added to
```
https://raw.githubusercontent.com/sparkfun/Arduino_Boards/master/IDE_Board_Manager/package_sparkfun_index.json
```
in File -> Preferences -> Additional Circuit Board Manager URLs. and select "SparkFun Pro Micro" card in the Tools -> Card section, then make sure that you also select the Processor option in the Tools section as ATmega32U4 (5V, 16MHz).

Also make sure that the Keyboard.cpp and Keyboard.h files in the "Source Code" directory are in the same directory as the Baduino.ino file.
