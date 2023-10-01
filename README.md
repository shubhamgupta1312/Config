# Config
Explore16/32mypic24ep512gu810
//this is my config file 
// PIC24FJ128GA010 Configuration Bit Settings

// CONFIG2
#pragma config POSCMOD = XT             // Primary Oscillator Select (XT Oscillator mode selected)
#pragma config OSCIOFNC = OFF           // Primary Oscillator Output Function (OSC2/CLKO/RC15 functions as CLKO (FOSC/2))
#pragma config FCKSM = CSDCMD           // Clock Switching and Monitor (Clock switching and Fail-Safe Clock Monitor are disabled)
#pragma config FNOSC = PRIPLL           // Oscillator Select (Primary Oscillator with PLL module (HSPLL, ECPLL))
#pragma config IESO = OFF               // Internal External Switch Over Mode (IESO mode (Two-Speed Start-up) disabled)

// CONFIG1
#pragma config WDTPS = PS32768          // Watchdog Timer Postscaler (1:32,768)
#pragma config FWPSA = PR128            // WDT Prescaler (Prescaler ratio of 1:128)
#pragma config WINDIS = ON              // Watchdog Timer Window (Standard Watchdog Timer enabled,(Windowed-mode is disabled))
#pragma config FWDTEN = OFF             // Watchdog Timer Enable (Watchdog Timer is disabled)
#pragma config ICS = PGx2               // Comm Channel Select (Emulator/debugger uses EMUC2/EMUD2)
#pragma config GWRP = OFF               // General Code Segment Write Protect (Writes to program memory are allowed)
#pragma config GCP = OFF                // General Code Segment Code Protect (Code protection is disabled)
#pragma config JTAGEN = OFF             // JTAG Port Enable (JTAG port is disabled)

// #pragma config statements should precede project file includes.
// Use project enums instead of #define for ON and OFF.

#include <xc.h>
#include <stdio.h>
#include <stdlib.h>


//S3,4,5,and 6 switches on the board
#define s3 PORTDbits.RD6
#define s6 PORTDbits.RD7
#define s5 PORTAbits.RA7    //Port A
#define s4 PORTDbits.RD13
#define s3_Control _TRISD6 
#define s6_Control _TRISD7
#define s5_Control _TRISA7  //Port A
#define s4_Control _TRISD13


void Delay(int Tdelay) // Tdelay is time in msec
{
    int TFLY;
    
    TFLY = Tdelay*(62.5);   // TFLY= Tdelay* (Fosc/2)/Presacler
                            // where Oscillator click is 32MHz
                            // Delay(500) = 500ms*(32MHz/2) / 256
    T1CON = 0x8030;         // Timer 1 is on with 256 PS
                            // use System Clock Fosc/2
    
    TMR1=0;
    while(TMR1<TFLY);
    
            
}
