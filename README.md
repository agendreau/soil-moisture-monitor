# Soil Moisture Monitor

## Introduction 
Now you will create a system to monitor the soil moisture in the pot of soil. You can use ``||music: speaker||`` to make a sound when the moisture is low. You can use the ``||neopixel: five LEDs||`` on the gator:bit or the ``||basic: LEDS||`` on the micro:bit. You will use the ``||logic: if then else||`` blocks to ask questions about the value of the ``||gatorSoil: soil moisture||`` to decide what you want to do. Lastly don't forget to think about ``||basic: how often||`` you want to take measurements, how you will ``||input: control||`` when the measurements are taken, and ``||loops: how many||`` measurements you want to take. Two potential solutions are in the Hint. When you think you've got it, ``|Download|`` the code and try it out.

```blocks
input.onButtonPressed(Button.A, function () {
    for (let i = 0; i < 4; i++) {
        basic.showNumber(Math.round(gatorSoil.moisture(AnalogPin.P2, GatorSoilType.Moisture, DigitalPin.P1) * 100))
        if (Math.round(gatorSoil.moisture(AnalogPin.P2, GatorSoilType.Moisture, DigitalPin.P1) * 100) < 60) {
            basic.showString("WATER")
            music.beginMelody(music.builtInMelody(Melodies.Dadadadum), MelodyOptions.Once)
            strip.showColor(neopixel.colors(NeoPixelColors.Yellow))
        } else {
            strip.showColor(neopixel.colors(NeoPixelColors.Green))
        }
        basic.pause(3600000)
    }
})
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P12, 5, NeoPixelMode.RGB)
basic.forever(function () {
    basic.showNumber(Math.round(gatorSoil.moisture(AnalogPin.P2, GatorSoilType.Moisture, DigitalPin.P1) * 100))
    if (Math.round(gatorSoil.moisture(AnalogPin.P2, GatorSoilType.Moisture, DigitalPin.P1) * 100) < 60) {
        basic.showString("WATER")
        basic.showIcon(IconNames.Sad)
        strip.showColor(neopixel.colors(NeoPixelColors.Yellow))
    } else {
        basic.showLeds(`
            . . . . .
            . # . # .
            . . . . .
            # . . . #
            . # # # .
            `)
        strip.showColor(neopixel.colors(NeoPixelColors.Green))
    }
    basic.pause(3600000)
})
```

```package
gatorSoil=github:sparkfun/pxt-gator-soil
neopixel=github:microsoft/pxt-neopixel
```






