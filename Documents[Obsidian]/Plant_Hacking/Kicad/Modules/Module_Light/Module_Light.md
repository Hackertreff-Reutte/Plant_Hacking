# Module Light

## Parts

Part         | Description       | Value     | Links
-------------|-------------------|-----------|------------
GH JTLPS1.24 | LED Hyper Red     | Hyper Red | [Mouser LED Hyper Red](https://www.mouser.at/ProductDetail/ams-OSRAM/GH-JTLPS124-K5L2-1-1-150-R33?qs=T94vaHKWudTV7nF1cL9Qdg%3D%3D "https://www.mouser.at/ProductDetail/ams-OSRAM/GH-JTLPS124-K5L2-1-1-150-R33?qs=T94vaHKWudTV7nF1cL9Qdg%3D%3D")
GD JTLPS1.14 | LED Deep Blue     | Deep Blue | [Mouser LED Deep Blue](https://www.mouser.at/ProductDetail/ams-OSRAM/GD-JTLPS114-MFN8-25-1-150-R33?qs=sGAEpiMZZMusoohG2hS%252B13XB79dZiCCb4Oh0%2F9PEIG6nbuQBvKP38A%3D%3D "https://www.mouser.at/ProductDetail/ams-OSRAM/GD-JTLPS114-MFN8-25-1-150-R33?qs=sGAEpiMZZMusoohG2hS%252B13XB79dZiCCb4Oh0%2F9PEIG6nbuQBvKP38A%3D%3D")
GF JTLPS1.24 | LED Far Red       | Far Red   | [Mouser LED Far Red](https://www.mouser.at/ProductDetail/ams-OSRAM/GF-JTLPS124-KXK5-1-1-150-R33?qs=T94vaHKWudRommpTngdQgA%3D%3D "https://www.mouser.at/ProductDetail/ams-OSRAM/GF-JTLPS124-KXK5-1-1-150-R33?qs=T94vaHKWudRommpTngdQgA%3D%3D")
*missing*    | LED White         | White     | *missing*
LM3410       | LED Driver        |           | [Mouser LM3410](https://www.mouser.at/ProductDetail/Texas-Instruments/LM3410YQMF-NOPB?qs=X1J7HmVL2ZG6pLs43DFr0A%3D%3D "https://www.mouser.at/ProductDetail/Texas-Instruments/LM3410YQMF-NOPB?qs=X1J7HmVL2ZG6pLs43DFr0A%3D%3D")
Inductor     | Inductor          | *missing* | *missing*
Resistor     | R_sense Resistors | *missing* | *missing*
Resistor     | PullUp Resistors  | 100k      | *missing*
Capacitor    | Input Capacitor   | *missing* | *missing*
Capacitor    | Output Capacitor  | *missing* | *missing*
Sottky Diode | Sottky Diode      |           | *missing* 


## Calculations

### R_sense

$\frac{V_{FB}}{R_{SET}} = I_{LED}$

sovle for $R_{SET}$ we get

$R_{SET} = \frac{V_{FB}}{I_{LED}}$

$V_{FB}$ is a constant with a minimul value of 178mV, typical value of 190mV and maximum value of 202mV.

For the calculations we will use 190mV for $V_{FB}$.

$I_{LED}$ is the current through the LEDs. We get this value from the Forward current diagram in the LED datasheet. We know that the LEDs has a typical power consumption of 0.5W (datasheet). So we can determine the max LED current and forward voltage so that it does not exceed 0.5W. 

$I_{LED_MAX} \simeq 150mA$
$VF_{MAX} \simeq 2.91V$

Theoretical max power: $Power = I_{LED_MAX} \times VF_{MAX} = 150mA \times 2.91V = 0.4365W$

Now we calculate the R_sense resistor:

$R_{SET} = \frac{V_{FB}}{I_{LED}} = \frac{190mV}{150mA} = 1.26666\ohm$

The next closest R12 value is $1.2\ohm$. If be back track we get the following values.

$I_{LED} = \frac{V_{FB}}{R_{SET}} = \frac{190mV}{1.2\ohm} = 158.3mA$

$I_{LED_MAX} = \frac{V_{FB_MAX}}{R_{SET}} = \frac{202mV}{1.2\ohm} = 168.3mA$

If we then get the forward voltage values from the datasheet for those to forward currents we get: 

$VF_{158.3mA} \simeq 2.92V$
$VF_{168.3mA} \simeq 2.93V$

So the typically and maximum power consumptions are:

$Power_{TYP} = 158.3mA \times 2.92V = 0.4622W$
$Power_{MAX} = 168.3mA \times 2.93V = 0.4931W$

Here we see that we are still around the expected power consumption and don't have to worry about it.