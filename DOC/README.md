
# How to test 4164 / 41256 with DRAM TESTER Arduino

## Quick procedure

Install a chip on tester

Push **START** button

LEDs (RED and GREEN) flashing during the test :high_brightness: :high_brightness:

:alarm_clock: A few moments later :alarm_clock:

:eight_spoked_asterisk: GREEN = RAM OK

:red_circle: RED = RAM ERROR

## Détailed test  

Install / Open Arduino IDE

Menu *"TOOLS"* 

Select Board: *"Arduino AVR Boards"*

**Arduino Nano** for this documentation


if you want a very slow refresh test then use "**slow**" TEST version

```
dramarduino_new_slowTEST.ino
```

if you want normal refresh test then use "**normal**" TEST version


```
dramarduino_new_normalTEST.ino
```

