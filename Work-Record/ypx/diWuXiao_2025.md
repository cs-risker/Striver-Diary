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

## System Optimization

In order to improve the system response speed as well as reduce the CPU burden, two refresh schemes for OLED were tested and compared respectively. The final choice is to use task notification management, which effectively reduces the refresh frequency and avoids unnecessary resource waste. It is planned to further use this scheme to manage the operation of sending and executing UHF RFID commands.

# April 29

## System Optimization & Motor Exploration

I used the difference in rotation pulses between the two wheels to perform a PID operation to compensate for the heading angle. Several attempts were made to no avail, so it was abandoned.

> dwx:
>
> 吭哧吭哧6小时，其结果啥也不是😤

# April 30

## PCB Print & Structure Modification

Draw a PCB schematic diagram, do the overall system planning, and strive to complete the PCB board drawing and board tomorrow. Modify the shape of the car, test the bus steering machine, and continue tomorrow.

# May 24

## Start an embedded practical project

Open an embedded practical project -- a samll desktop screen. The whole process of learning and practice from 0 to 1, the goal is to achieve personalized design as another "graduation design" for me.

> 桌面屏幕项目：[教学视频](https://www.bilibili.com/video/BV1wV4y1G7Vk/?spm_id_from=333.1387.homepage.video_card.click&vd_source=df944b7260e2006a48d19f043b2b102e)、[飞书文档](https://x509p6c8to.feishu.cn/docx/NQCTdjUFJoYoZ1xYHS9cIlbwnxh)
>
> 小智学长其他项目：[AI助手](https://x509p6c8to.feishu.cn/wiki/ItJUwTtOhi1AH0kYwngccoPUnke)、[打印机](https://www.youtube.com/watch?v=JzEihLGG-iM&list=PLyL9zpk37wNEyxaWGSZHCoqLcyOevt3Sk&index=17&themeRefresh=1)

# May 25

## Hardware Composition

![hardware composition](https://github.com/cs-risker/Striver-Diary/blob/main/Work-Record/ypx/picture/hardware%20composition.png)

# May 26

## Project Postponement

After in-depth understanding of the "desktop screen" project, I feel that the project is not highly customizable and the lack of hardware materials at hand leads to the cost exceeding expectations (within 100), so I plan to temporarily strand the project and select the project according to the existing materials at hand.
