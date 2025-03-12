# Notes for Kilo Project

### Chapter 2 - Entering Raw Mode

Usual Command-Line Input is what we call canonical or cooked mode where user input is set to the program after ENTER key is pressed.
Complex interfaces require RAW mode where each keystroke can be handled by the program itself giving us more control.
Turning on RAW mode requires multiple steps and fliping different flags.

> unistd.h - standard symbolic constants and types

Reading: We Will read only one character at a time using read(STDIN_FILENO, 1, &c)
Note:- we are reading one character at a time input is still being fed one line at a time.

Turning of ECHO: Ever noticed how when you type your password in sudo, your password doesn't show. That is because the echo mode which is by default on is turned off.

> termios.h - define values for teminal IO interfaces

termios struct provided by termios.h can store attributes of terminal configuration.
tcgetattr reads attributes of current terminal configuration into termios struct raw.

we can then modify attributes in raw:
c_lflag: local flags
we bitwise and it with a negation of echo flag effectively masking echo flag while keeping others same.

tcsetattr allows us to set attributes given by termios struct raw to the current terminal configuration.