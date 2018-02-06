# MicroPython Kitchen Sink for M5Stack

![M5Stack](https://appelsiini.net/img/m5-wires-1400.jpg)

This repository contains few abstractions and helper libraries to help jumpstarting a MicroPython project with [M5Stack development kit](http://www.m5stack.com/). All development is done using [Loboris fork](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo) of MicroPython. Everything is still evolving. Code should be considered alpha quality. BC breaks will happen.

Use `make sync` to upload files to the board. Not that you must have [rshell](https://github.com/dhylands/rshell) installed. After uploading `make repl` accesses the serial repl.

```shell
$ sudo pip3 install rshell
$ make sync
$ make repl
```

The file `main.py` will contain the kitchen sink example. Helper libraries and absractions are in `lib` folder.

## Display

Light weight wrapper for [Loboris TFT module](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/display)  which retains all the original api and properties but adds a few helper methods. See [Loboris wiki](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/display) for documentation.

```python
import m5stack
tft = m5stack.Display()

tft.text(tft.CENTER, 45,        "`7MMM.     ,MMF'       \n")
tft.text(tft.CENTER, tft.LASTY, "  MMMb    dPMM         \n")
tft.text(tft.CENTER, tft.LASTY, "  M YM   ,M MM  M******\n")
tft.text(tft.CENTER, tft.LASTY, "  M  Mb  M' MM .M      \n")
tft.text(tft.CENTER, tft.LASTY, "  M  YM.P'  MM |bMMAg. \n")
tft.text(tft.CENTER, tft.LASTY, "  M  `YM'   MM      `Mb\n")
tft.text(tft.CENTER, tft.LASTY, ".JML. `'  .JMML.     jM\n")
tft.text(tft.CENTER, tft.LASTY, "               (O)  ,M9\n")
tft.text(tft.CENTER, tft.LASTY, "                6mmm9  \n")
tft.text(tft.CENTER, tft.LASTY, "                       \n")
tft.text(tft.CENTER, tft.LASTY, "https://appelsiini.net/")
```

Helper methods for turning the display on and off. Under the hood this just sets `TFT_LED_PIN` high or low.

```python
tft.on()
tft.off()
```

## Buttons

Abstraction for the provided buttons using IRQ. Default is `IRQ_FALLING` ie. when button was pressed. You can also use `IRQ_RISING` and `IRQ_RISING | IRQ_FALLING`.

```python
a = m5stack.ButtonA(
    callback=lambda pin: print("Button A pressed.")
)

b = m5stack.ButtonB(
    trigger=Pin.IRQ_RISING,
    callback=lambda pin: print("Button B released.")
)

c = m5stack.ButtonC(callback=button_handler())

def button_hander(pin):
    print("Button C pressed.")
```

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.