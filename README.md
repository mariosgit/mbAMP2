# mbAMP2

A fully digital audio amplifier.

This one needs some I2C talking to start up.
You will also need some kind of I2S data source, e.g. Teensy Audio, some china ADC or SPDIF receiver.

## Status

Test Log:
* Hooked up as Teensy Audio Output.
* I2C getting responses.
* It turns on and puts out some kinda sound...

## Minimum Startup Code

```
bool Tas5805m::begin()
{
    Wire.begin();
    write(DEVICE_CTRL_2, 0x02);  // HiZ
    delay(5);
    write(DEVICE_CTRL_2, 0x03);  // Play
}
void Tas5805m::write(byte reg, byte data)
{
    Wire.beginTransmission(_adr);
    Wire.write(reg);
    Wire.write(data);
    byte result = Wire.endTransmission();
    logerror(result, reg);
}
```
