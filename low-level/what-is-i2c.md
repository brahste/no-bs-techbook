# What is I2C?

Protocol for sending data back and forth. Used in microcontrollers, different memories, temperatrue sensors, ADCs, and integrated circuits.

SImple impl, one master 1 slave. Only 2 pins (SCL) clock (SDA) data. Clock is used to align data so slave know when to sample it. Can also have multiple slaves on a single bus. You could be sending commands to a DAQ, or an ADC, or another microcontroller.

Advantages/disadvatnges

Ad: low pin count
ad: addressing built in
ad: ubiquitius

dis: half-duplex, 400 kbps max, half duplex means limited on bandwidth, not as fast as SPI
dis: careful consideration of hardware
dos: more complicated than spi or UART

Notes:
- The slave uses the clock to know when to sample the data line

## Coding

On linux you can interact with I2C buses using the `i2c-tools` program suite.

`i2cdetect -l` lists the I2C busses available on the system.

useful tools in this suite include `i2cdetect`, `i2cget`, `i2cset`, `i2cdump`, `i2ctransfer`.

# What is SPI?

Serial Peripheral Interface is extremely common for intergrated circuits (ICs). Used in memory chips, things like SD cards, lots of microcontrollers, IO expandeders, LCDs, DAQs, ADCs. SPI has a clock, interfaces with a clock can generally transmit faster. 

There is a master and slaves, the IC is the SPI sslave where the master is a microcontroller or FPGA, the master initiationes the interaction with 4 signals. SCLK - serial clock, MOSI - master out slave in, MISO - master in slave out, SS - slave select (or chip select) which is active low. 

You can have muleiple slaves on the same line. In this case there are three SS (chip select lines). Think of it as a way for the slave/chip to open it's eye and read the data.

Advantages/disadvantages:

ad: full duplex, e.g. can send and receive at same time.
ad: higher spped that UART or I2C
ad: Ubiquitous

dis: More pins that UART or I2C
dis: short distances vs. RS-485/RS-232
dis: lots of variants


