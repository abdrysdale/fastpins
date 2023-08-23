# Fastpins

Fastpins is a simple C library to provide Python with microsecond precision when triggering GPIO pins on a RaspberryPi.

The project was designed for pseudo-simulateneously triggering a laser and camera but can be adapted for other uses.

## Example

- First the GPIO pins need to be initialised with:

```python
import fastpins as fp
fp.init()
```
which sets up the GPIO pins with physical pin naming convention.

- Next, the pins to be used need to be set up with:

```python
laser_trigger_pin = 22
pin_value = 1 # Use 1 for writing, 0 for reading
pin_pud = 0 # Only used for read pins, 0 = no resistor, 1 = pull up resistor, 2 = pull down resistor

fp.setpin(laser_trigger_pin, pin_value, pin_pud)
```

- The pins can then either be fired as a pulse (delay, turned on, wait for a duration and then turned off) with:

```python
delay = 40000       # Delay in microseconds.
duration = 200000   # Duration in microseconds.
pin_1 = 22
pin_2 = 8
fp.pulse(delay, duration, pin_1, pin_2)
```

- Alternatively, the pins can be pulsed via edge detection (delay, turned on, wait for a signal from a read pin and then turned off):

```python
delay = 40000       # Delay in microseconds.
pin_1 = 22
pin_2 = 8
pin_read = 12
fp.pulse(delay, pin_1, pin_2, pin_read)
```

