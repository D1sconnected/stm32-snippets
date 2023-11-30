# shift_reg_gpio_test

Control 7-digit (common anode) with 74HC595 IC.

# Wiring 
```
 STM32F103 (Blue Pill)                  74HC595
+-----------------------+              +-------------------+
|                    GND+--------------+GND  (8)           |
|                       |              |                   |
|                    3V3+--------------+VCC  (16)          |
|                       |              |                   |
|               (PA7) DO+--------------+DS   (14)          |
|                       |              |                   |
|               (PA4) CS+--------------+STCP (12)          |
|                       |              |                   |
|             (PA5) SHCP+--------------+SHCP (11)          |
|                       |              |                   |
+-----------------------+              |                   |
                               3V3-----+#MR   (10)         |
                                       |                   |
                               GND-----+#OE   (13)         |
                                       +-------------------+
```

# Functions

* `int ShifRegister_Clear()` -  Clear all 7-digit LEDs
* `int ShiftRegister_Set (uint8_t val)` -  Set byte to shift-register
* `int ShiftRegister_Strob ()` -  Latch value

# Example

```
  // Display values from 0 to F
  ShifRegister_Clear();
  uint8_t numbers[16] = {~0x3F, ~0x06, ~0x5B, ~0x4F, ~0x66, ~0x6D, ~0x7D, ~0x07, ~0x7F, ~0x6F, ~0x77, ~0x7C, ~0x39, ~0x5E, ~0x79, ~0x71}; // 0-F
  while (1)
  {
      for(int i=0; i<sizeof(numbers); i++)
       {
    	  	  ShiftRegister_Set (numbers[i]);
    	  	  ShiftRegister_Strob();
               HAL_Delay(1000);
       }
  }
}
```
