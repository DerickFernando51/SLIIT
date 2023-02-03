# Driving MAX7221 LED seven-segment display using PIC16F877A
# Abstract
The aim of this project is to display the EN number on a seven segment display. For this
task the PIC16F877A microcontroller and drive/control LED Seven Segment Display MAX7221
was used. Assembler was used as the programming language. The circuit was constructed
using Proteus simulation software.

# Introduction
MAX7221 is a compact, serial input/output common-cathode display driver that interfaces
microcontrollers to 7-segment numeric LED displays of up to 8 digits. This chip is compatible
with SPI and many serial communication protocols. This chip needs only 3 control lines from
your microcontroller to drive the display. Seven segment displays are used for devices such as
bar graph displays, industrial controllers, panel meters and LED matrix displays. The seven
segments are assigned letters from A to G. There is an optional decimal point that can be used
to display non integer numbers.

# Objectives
• Identify the features and functions of the Max 7221 display driver

• Become proficient in programming microcontrollers using assembly

• Learn the principles of circuit design

• Understand the applications of seven segment displays

# Methodology
<img width="136" alt="image" src="https://user-images.githubusercontent.com/124335793/216532629-2b5e8a6d-47cd-4ecc-b64e-0abf4340bf20.png">





# Code
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
