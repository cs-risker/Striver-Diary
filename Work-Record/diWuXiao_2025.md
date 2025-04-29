# April 27

## OLED Driver

Learn and port the EspressIf official SSD1306 driver to the RFIDCar project to display the auto/manual mode ("Auto"/"Manual") and the car's current motion status ("Normal"/"Abnormal") on the OLED  (128 * 32)  screen.

> Interesting projects:
>
> https://github.com/nopnop2002/esp-idf-ssd1306/tree/master
>
> My GitHub projects:
>
> https://github.com/isWuXiao/espressif__ssd1306
>
> Good reference:
>
> https://blog.csdn.net/xundh/article/details/132346497

# April 28

In order to improve the system response speed as well as reduce the CPU burden, two refresh schemes for OLED were tested and compared respectively. The final choice is to use task notification management, which effectively reduces the refresh frequency and avoids unnecessary resource waste. It is planned to further use this scheme to manage the operation of sending and executing UHF RFID commands.

# April 29

I used the difference in rotation pulses between the two wheels to perform a PID operation to compensate for the heading angle. Several attempts were made to no avail, so it was abandoned.

> dwx:
>
> 吭哧吭哧6小时，其结果啥也不是😤
