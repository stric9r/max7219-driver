# max7219-driver  
Serially interfaced 8 digit LED display driver  

## General Usage  
This driver is for the max7219 serial display driver.  See datasheet in this repository for more details of how the chip functions.  
See this repository for an example of how this is used: https://github.com/stric9r/Line6-FBV3-Clone  

### Initialization  
Call the max7219_init(...) function to intialize the module.  
Make sure to pass a function pointers for writing to GPIO in the proper format.  

Arbritraty function names to convey this example:  
set_gpio(gpio_pin, value) -> f_write(int, int)  
spi_write(data) -> f_write(int)  
delay_blocking(micro_seconds) -> f_delay_us(unsigned int)  
```  
//Bit banging init  
max7219_init(set_gpio,            ///fp to write gpio  
             NULL,                ///no serial  
             delayMicroseconds,   ///fp blocking to simulate clock  
             MAX7219_DIN,         ///gpio pin  
             MAX7219_CLK,         ///gpio pin  
             MAX7219_LD,          ///gpio pin  
             MAX7219_DECODE_NONE, ///decode setting, see datasheet   
             INTENSITY_8,         ///intensitly setting, see datasheet    
             SCAN_LIMIT_2);       ///scan limit setting, see datasheet  
```  
The time for clock pulses is set with the define `CLK_WIDTH_US`.  
Change it to accomodate your needs.  
```  
//Serial init  
max7219_init(set_gpio,             ///fp to write gpio  
             spi_write,            ///fp to serial write interface  
             NULL,                 ///no delay  
             0,                    ///gpio pin - not used  
             0,                    ///gpio pin - note used  
             MAX7219_LD,           ///gpio pin - to load the command  
             MAX7219_DECODE_NONE,  ///decode setting, see datasheet  
             INTENSITY_8,          ///intensitly setting, see datasheet  
             SCAN_LIMIT_2);        ///scan limit setting, see datasheet  
```  

### Control  
Below are all the functions you can use to control the led output.  
```  
void max7219_set_digit_bcd(enum max7219_digits const digit, uint8_t bcd, bool const decimal_point);  
void max7219_set_digit_segment(enum max7219_digits const digit,  
                               enum max7219_segments segment,  
                               bool state);  
void max7219_clear_all(void);  
void max7219_clear_digit(enum max7219_digits const digit);  
void max7219_set_display_test(enum max7219_display_tests const mode);  
```  
### Settings  
Below are all the functions you can use to change settings.  
When changing any settings, make sure to call `void max7219_set_mode(enum max7219_modes const mode)` and specify SHUTDOWN MODE first.  
```  
void max7219_set_decode_mode(uint8_t mode);  
void max7219_set_intensity(enum max7219_intensities intensity);  
void max7219_set_scan_limit(enum max7219_scan_limits const scan_limit);  
void max7219_set_mode(enum max7219_modes const mode);  
```  



