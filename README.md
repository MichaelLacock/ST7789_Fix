# ST7789_Fix

This is a fix for screen rotation for the Adafruit EyeSPI 1.69" 280x240 tft
for the "Adafruit ST7735 and ST7789" Arduino Library.  

Currect Problem:
When rotating the screen using "tft.setRotation(3);" the display rowstart is off.

Additions:

- Addidtion to "Adafruit_ST7789.cpp":

      // off-set selector added by Michael Lacock, 2021
      void Adafruit_ST7789::rowOffset(uint8_t n1, uint8_t n2, uint8_t n3, uint8_t n4) {
        _rowstart = n1;
        _colstart = n2;
        _xstart = n3;
        _ystart = n4;
      }
      
- Addidtion to "Adafruit_ST7789.h":
      void rowOffset(uint8_t n1, uint8_t n2, uint8_t n3, uint8_t n4);
      
How this fix works:
Assuming you have "Adafruit_ST7789 tft = Adafruit_ST7789(TFT_CS, TFT_DC, TFT_RST);" at the
top of your sketch, tft.rowOffset(0, 0, 20, 0); will offset it back to the correct spot
for tft.setRotation(3); by 20 pixels for the X coordinate.

Layout:
tft.rowOffset(_rowstart, _colstart, _xstart, _ystart);
The _rowstart and _colstart can remain 0, they don't actually do anything in this use case.

I'm includeing the moddified files here too so you can replace them in the "Adafruit_ST7735_and_ST7789_Library"
folder in your Arduino Libraries folder.  Please note that this is a modification of code originally 
writen by Adafruit Industries.

