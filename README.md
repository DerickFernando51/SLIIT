# Driving MAX7221 LED seven-segment display using PIC16F877A
# 1.0 Abstract
The aim of this project is to display the EN number on a seven segment display. For this
task the PIC16F877A microcontroller and drive/control LED Seven Segment Display MAX7221
was used. Assembler was used as the programming language. The circuit was constructed
using Proteus simulation software.

# 2.0 Introduction
MAX7221 is a compact, serial input/output common-cathode display driver that interfaces
microcontrollers to 7-segment numeric LED displays of up to 8 digits. This chip is compatible
with SPI and many serial communication protocols. This chip needs only 3 control lines from
your microcontroller to drive the display. Seven segment displays are used for devices such as
bar graph displays, industrial controllers, panel meters and LED matrix displays. The seven
segments are assigned letters from A to G. There is an optional decimal point that can be used
to display non integer numbers.

# 3.0 Objectives
• Identify the features and functions of the Max 7221 display driver

• Become proficient in programming microcontrollers using assembly

• Learn the principles of circuit design

• Understand the applications of seven segment displays

# 4.0 Methodology

# 4.1 Pin configuration and selection

  
   <img width="824" alt="image" src="https://user-images.githubusercontent.com/124335793/216533938-177446b8-d6e9-4d39-80f0-0d2e9f554fd4.png">



➢ Pins 1, 12 and 13 were used to feed data into the MAX7221 display.The ports of the pic16F877A were selected as follows:
 
     • Port B, pin 1 – CLK
 
     • Port B, pin 2 – CS
  
     • Port B, pin 3 – DIN

➢ The seven segments A to G and the decimal point were connected to the display

➢ The DIG 0 -DIG 7 pins were also connected to the display as shown above.

➢ The ISET pin was connected to the VDD through a resistor

# 4.2 Data format
<img width="737" alt="image" src="https://user-images.githubusercontent.com/124335793/216534882-28e1904b-c917-43f8-80b5-96cfa9d47fad.png">

The MAX7221 display has a 16 bit serial data format. The bits from 11 to 8 specify the address
of the data. The next 8 bits contain the data.

# 4.3 Initialization of registers
<img width="759" alt="image" src="https://user-images.githubusercontent.com/124335793/216535346-d3c4bcdd-785a-43b3-af6a-107d4e05eb88.png">

The MAX7221 has 5 registers that should be initialized before data can be fed.

    • Shutdown register

    • Decode mode register

    • Intensity register

    • Scan limit register

    • Display test register

# 4.3.1 Shutdown register
<img width="914" alt="image" src="https://user-images.githubusercontent.com/124335793/216535669-dcd8efb0-f387-4e4c-a888-ba56af62b589.png">

  • The address of this register is (0xXC)
 
  • The normal operation mode was selected (0x01)
  
# 4.3.2 Decode mode register

<img width="914" alt="image" src="https://user-images.githubusercontent.com/124335793/216536289-ff7c1151-42fc-41b7-97bd-81f1a17fe484.png">

• The address of this register is (0xX9)

• Code B decode for digits 7-0 was selected (0xFF)

# 4.3.3 Display test register

<img width="913" alt="image" src="https://user-images.githubusercontent.com/124335793/216536808-09dab430-84b9-48c4-8d29-a3eb28bc4c5c.png">

• The address of this register is (0xXF)

• The normal operation mode was selected (0x00)

# 4.3.4 Intensity register
<img width="762" alt="image" src="https://user-images.githubusercontent.com/124335793/216537222-55ac608b-3764-48ce-b141-ca76ff50495e.png">

• The address of this register is (0xXA)

• The maximum brightness was selected (0xXF)

# 4.3.5 Scan limit register
<img width="760" alt="image" src="https://user-images.githubusercontent.com/124335793/216537447-5cad3092-1cb5-4298-a397-6bdedaf3e957.png">

• The address of this register is (0xXB)

• The option to display digits 0-7 was selected (0xX7)


# 4.4 Circuit set up
<img width="915" alt="image" src="https://user-images.githubusercontent.com/124335793/216537785-bfe2bfef-24ee-45bc-b5ec-c48cbab3d355.png">

Components used:

      • MAX7221 display driver
    
      • PIC16F877A microcontroller
    
      • 7 segment, 8 digit cathode display
    
      • Crystal oscillator
# 5.0 Code
  ; PIC16F877A Configuration Bit Settings

; Assembly source line config statements

; CONFIG
  CONFIG  FOSC = HS             ; Oscillator Selection bits (HS oscillator)
  CONFIG  WDTE = OFF            ; Watchdog Timer Enable bit (WDT disabled)
  CONFIG  PWRTE = OFF           ; Power-up Timer Enable bit (PWRT disabled)
  CONFIG  BOREN = OFF           ; Brown-out Reset Enable bit (BOR disabled)
  CONFIG  LVP = OFF             ; Low-Voltage (Single-Supply) In-Circuit Serial Programming Enable bit (RB3 is digital I/O, HV on MCLR must be used for programming)
  CONFIG  CPD = OFF             ; Data EEPROM Memory Code Protection bit (Data EEPROM code protection off)
  CONFIG  WRT = OFF             ; Flash Program Memory Write Enable bits (Write protection off; all program memory may be written to by EECON control)
  CONFIG  CP = OFF              ; Flash Program Memory Code Protection bit (Code protection off)

// config statements should precede project file includes.
#include <xc.inc>
;--------initializing----------------  
  
 //PSECT start, CLASS = CODE, DELTA=2
 start:
    PAGESEL MAIN
    GOTO MAIN
    
    PSECT CODE, DELTA=2
 
 ;-----------end initializing---------

     
   BSF STATUS, 5;Bank 1
   BCF TRISB,1 ;CLK
   BCF TRISB,2 ;CS
   BCF TRISB,3;DLN  
   BCF STATUS,5; Bank 0  
  
MAIN:  
   
    //Shutdown-register(0x0C)	Normal operation(0x00)
    BCF PORTB,2;//CS-0 
    BCF PORTB,3 //DLN-0	    15
    BSF PORTB,1//CLK-1
    BCF PORTB,1//CLK-0 
    BCF PORTB,3 //	    14
    BSF PORTB,1       
    BCF PORTB,1       
    BCF PORTB,3  //	    13
    BSF PORTB,1      
    BCF PORTB,1     
    BCF PORTB,3//	    12
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3 //	    11
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//	    10
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	    9
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	    8
    BSF PORTB,1;
    BCF PORTB,1
    BCF PORTB,3//	    7
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	    6
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	    5
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	    4
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	    3
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	    2
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	    1
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//	    0
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,2//CS-1
    
    //Decode mode register(0x09)	Decode 0-7(0xFF)
    BCF PORTB,2   
    BCF PORTB,3//   15
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   14
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   13
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   12
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   11
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   10
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   9
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   8
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   7
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   6
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   5
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   4
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   3
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   2
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   1
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   0
    BSF PORTB,1
    BCF PORTB,1    
    BSF PORTB,2    
   
    
    //Intensity register(0xXA)	Maximum brightness(0xXF)
    BCF PORTB,2    
    BCF PORTB,3//   15
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   14
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   13
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   12
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   11
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   10
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   9
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   8
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   7
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   6
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   5
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   4
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   3
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   2
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   1
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   0
    BSF PORTB,1
    BCF PORTB,1    
    BSF PORTB,2
    
     //Scan limit register(0xXB)	Display digits 0-7(0x07)    
    BCF PORTB,2    
    BCF PORTB,3//   15
    BSF PORTB,1       
    BCF PORTB,1       
    BCF PORTB,3//   14
    BSF PORTB,1       
    BCF PORTB,1     
    BCF PORTB,3//   13
    BSF PORTB,1      
    BCF PORTB,1    
    BCF PORTB,3//   12
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   11
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   10
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   9
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   8
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   7
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   6
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   5
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   4
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   3
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   2
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   1
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   0
    BSF PORTB,1
    BCF PORTB,1 
    BSF PORTB,2 
      
 
    //Display test register(0xXF)	Normal mode(0x00)    
    BCF PORTB,2    
    BCF PORTB,3//	15
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	14
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	13
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	12
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//	11
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//	10
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//	9
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//	8
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	7
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	6
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	5
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	4
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	3
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	2
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	1
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//	0
    BSF PORTB,1
    BCF PORTB,1   
    BSF PORTB,2 
    
    //DIGITS
    //digit0 - 2  
    BCF PORTB,2    
   
    BCF PORTB,3//   15
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   14
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   13
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   12
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   11
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   10
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   9
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   8
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   7
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   6
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   5
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   4
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   3
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   2
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   1
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   0
    BSF PORTB,1
    BCF PORTB,1    
    BSF PORTB,2   
    
    //digit1 - 1    
    BCF PORTB,2   
    BCF PORTB,3//   15
    BSF PORTB,1	
    BCF PORTB,1	
    BCF PORTB,3//   14
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   13
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   12
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   11
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   10
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   9
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   8
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   7
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   6
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   5
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   4
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   3
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   2
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   1
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   0
    BSF PORTB,1
    BCF PORTB,1  
    BSF PORTB,2    
    
    //digit 2 - 4   
    BCF PORTB,2   
    BCF PORTB,3//   15
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   14
    BSF PORTB,1
    BCF PORTB,1	
    BCF PORTB,3//   13
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   12
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   11
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   10
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   9
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   8
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   7
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   6
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   5
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   4
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   3
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   2
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   1
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   0
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,1    
    BSF PORTB,2    
    
    //digit3 - 8 
    BCF PORTB,2   
    BCF PORTB,3//   15
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   14
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   13
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   12
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   11
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   10
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   9
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   8
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   7
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   6
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   5
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   4
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   3
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   2
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   1
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   0
    BSF PORTB,1
    BCF PORTB,1  
    BSF PORTB,2    
    
    //digit4 - 5
    
    BCF PORTB,2    
    BCF PORTB,3//   15
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   14
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   13
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   12
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   11
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   10
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   9
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   8
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   7
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   6
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   5
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   4
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   3
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   2
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   1
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   0
    BSF PORTB,1
    BCF PORTB,1   
    BSF PORTB,2    
    
    //digit5 - 8  
    BCF PORTB,2  
    BCF PORTB,3//   15
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   14
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   13
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   12
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   11
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   10
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   9
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   8
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   7
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   6
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   5
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   4
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   3
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   2
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   1
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   0
    BSF PORTB,1
    BCF PORTB,1  
    BSF PORTB,2    
    
    //digit6 - 8
    BCF PORTB,2    
    BCF PORTB,3//   15
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   14
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   13
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   12
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   11
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   10
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   9
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   8
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   7
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   6
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   5
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   4
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   3
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   2
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   1
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   0
    BSF PORTB,1
    BCF PORTB,1    
    BSF PORTB,2    
    
    //digit7 - 6    
    BCF PORTB,2    
    BCF PORTB,3//   15
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   14
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   13
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   12
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   11
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   10
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   9
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   8
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   7
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   6
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   5
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   4
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   3
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   2
    BSF PORTB,1
    BCF PORTB,1
    BSF PORTB,3//   1
    BSF PORTB,1
    BCF PORTB,1
    BCF PORTB,3//   0
    BSF PORTB,1
    BSF PORTB,1 
    BSF PORTB,2
      
GOTO MAIN
# 6.0 Output

<img width="915" alt="image" src="https://user-images.githubusercontent.com/124335793/216538236-23e644ec-e6db-4868-814d-b8f4f1545bef.png">

# 7.0 Conclusion

The task of this project was to display the EN number on a seven segment display. This was
achieved by programming the PIC16F877A microcontroller using the mplab software. The
Proteus simulation software was used to construct the circuit and ensure that the required
output is obtained. The MAX7221 display driver was used to interface the microcontroller to
the display.
