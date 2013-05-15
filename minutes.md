LED-digital-clock-7-segments-display
====================================

MSP430 code for minutes and hours
#include <msp430g2432.h>

#define pin1 BIT0
#define pin2 BIT1
#define pin3 BIT2
#define pin4 BIT3
#define pin5 BIT0
#define pin6 BIT1
#define pin7 BIT2
#define pin8 BIT3

char fracsec = 0; // local variable which counts up fractions of seconds
// based on the ticks from the interrupt
int sec = 0, min = 0, hour = 0;
void counter(void)
{
TA0CCR0 = 50000;// Count limit 1MHz / 50000 = 20, therefore interrupt triggers roughly every 50mS
TA0CCTL0 = CCIE;// Enable counter interrupts
TA0CTL = TASSEL_2 + MC_1;// Timer A 0 with SMCLK at 1MHZ, count UP
_BIS_SR( GIE);// Enable interrupts
}
#pragma vector=TIMER0_A0_VECTOR
__interrupt void Timer0_A0 (void) // Timer0 A0 interrupt service routine
{
fracsec++; // increment the fracsec counter by 1/if (fracsec == 20) // if fracsec is xx then

if(fracsec==20)
  {
	
	++sec;
	fracsec = 0; // reset the fracsec counter
	}
if (sec==60)// (1) increment sec - (2) is sec == 60
	{

	++min;
	sec = 0; // reset the sec counter
	}
if (min == 60) // (1) increment min - (2) is min == 60
      {
	//  ++hour;
	  min = 0; // reset the min counter
      }
/*if (hour == 24) // (1) increment hour - (2) is hour == 60
     {

     hour = 0; // reset the hour counter

     }*/


}



int main(void)
{
	WDTCTL = WDTPW + WDTHOLD; // Stop watchdog timer
    // Init Clock Module
        if (CALBC1_1MHZ != 0xFF)
        {
            DCOCTL = 0x00;
            BCSCTL1 = CALBC1_1MHZ;        // Calibrate clock at 1MHz
            DCOCTL = CALDCO_1MHZ;
        }

    P1DIR |= pin1 + pin2 + pin3 + pin4; // Assign as output
    P2DIR |= pin5 + pin6 + pin7 + pin8; // Assign as output
P1OUT = pin1 + pin3;
P2OUT = pin8;

    counter();

    while(1)
    {
 if(min==1)
      {
	 P2OUT = pin5;
      }
 if(min==2)
      {
	 P2OUT = pin6;
      }
 if(min==3)
       {
	 P2OUT = pin5 + pin6;
       }
 if(min==4)
 {
	 P2OUT = pin7;

 }
 if(min==5)
 {
	 P2OUT = pin5 + pin7;
 }
  if(min==6)
  {
	  P2OUT= pin6 + pin7;
  }
  if(min==7)
  {
	  P2OUT = pin5 + pin6 + pin7;
  }
  if(min==8)
  {
	  P2OUT = pin8;
  }
  if(min==9)
  {
	  P2OUT = pin5 + pin8;
  }
  if(min==10)
  {
	  P1OUT = pin1;
	  P2OUT = 0x00;

  }
  if(min==11)
  {
	  P1OUT = pin1;
	  P2OUT = pin5;
  }
  if(min==12)
  {
	  P1OUT = pin1;
	  P2OUT = pin6;
  }
  if(min==13)
  {
	  P1OUT = pin1;
	  P2OUT = pin5 + pin6;
  }
  if(min==14)
  {
	  P1OUT = pin1;
	  P2OUT = pin7;
  }
  if(min==15)
  {
	  P1OUT = pin1;
	  P2OUT = pin5 + pin7;
  }
  if(min==16)
  {
	  P1OUT = pin1;
	  P2OUT = pin6 + pin7;
  }
  if(min==17)
  {
	  P1OUT = pin1;
	  P2OUT = pin5 + pin6 + pin7;
  }
  if(min==18)
  {
	  P1OUT = pin1;
	  P2OUT = pin8;
  }
  if(min==19)
  {
	  P1OUT = pin1;
	  P2OUT = pin5 + pin8;
  }
  if(min==20)
  {
	  P1OUT = pin2;
	  P2OUT = 0x00;
  }
  if(min==21)
    {
  	  P1OUT = pin2;
  	  P2OUT = pin5;
    }
    if(min==22)
    {
  	  P1OUT = pin2;
  	  P2OUT = pin6;
    }
    if(min==23)
    {
  	  P1OUT = pin2;
  	  P2OUT = pin5 + pin6;
    }
    if(min==24)
    {
  	  P1OUT = pin2;
  	  P2OUT = pin7;
    }
    if(min==25)
    {
  	  P1OUT = pin2;
  	  P2OUT = pin5 + pin7;
    }
    if(min==26)
    {
  	  P1OUT = pin2;
  	  P2OUT = pin6 + pin7;
    }
    if(min==27)
    {
  	  P1OUT = pin2;
  	  P2OUT = pin5 + pin6 + pin7;
    }
    if(min==28)
    {
  	  P1OUT = pin2;
  	  P2OUT = pin8;
    }
    if(min==29)
    {
  	  P1OUT = pin2;
  	  P2OUT = pin5 + pin8;
    }
    if(min==30)
    {
  	  P1OUT = pin1 + pin2;
  	  P2OUT = 0x00;
    }
    if(min==31)
      {
    	  P1OUT = pin1+  pin2;
    	  P2OUT = pin5;
      }
      if(min==32)
      {
    	  P1OUT = pin1 + pin2;
    	  P2OUT = pin6;
      }
      if(min==33)
      {
    	  P1OUT = pin1 + pin2;
    	  P2OUT = pin5 + pin6;
      }
      if(min==34)
      {
    	  P1OUT = pin1 + pin2;
    	  P2OUT = pin7;
      }
      if(min==35)
      {
    	  P1OUT = pin1 + pin2;
    	  P2OUT = pin5 + pin7;
      }
      if(min==36)
      {
    	  P1OUT = pin1 + pin2;
    	  P2OUT = pin6 + pin7;
      }
      if(min==37)
      {
    	  P1OUT = pin1 + pin2;
    	  P2OUT = pin5 + pin6 + pin7;
      }
      if(min==38)
      {
    	  P1OUT = pin1 + pin2;
    	  P2OUT = pin8;
      }
      if(min==39)
      {
    	  P1OUT = pin1 + pin2;
    	  P2OUT = pin5 + pin8;
      }
      if(min==40)
      {
    	  P1OUT = pin3;
    	  P2OUT = 0x00;
      }
      if(min==41)
        {
      	  P1OUT = pin3;
      	  P2OUT = pin5;
        }
        if(min==42)
        {
      	  P1OUT = pin3;
      	  P2OUT = pin6;
        }
        if(min==43)
        {
      	  P1OUT = pin3;
      	  P2OUT = pin5 + pin6;
        }
        if(min==44)
        {
      	  P1OUT = pin3;
      	  P2OUT = pin7;
        }
        if(min==45)
        {
      	  P1OUT = pin3;
      	  P2OUT = pin5 + pin7;
        }
        if(min==46)
        {
      	  P1OUT = pin3;
      	  P2OUT = pin6 + pin7;
        }
        if(min==47)
        {
      	  P1OUT = pin3;
      	  P2OUT = pin5 + pin6 + pin7;
        }
        if(min==48)
        {
      	  P1OUT = pin3;
      	  P2OUT = pin8;
        }
        if(min==49)
        {
      	  P1OUT = pin3;
      	  P2OUT = pin5 + pin8;
        }
        if(min==50)
        {
      	  P1OUT = pin1 + pin3;
      	  P2OUT = 0x00;
        }
        if(min==51)
          {
        	  P1OUT = pin1 + pin3;
        	  P2OUT = pin5;
          }
          if(min==52)
          {
        	  P1OUT = pin1 + pin3;
        	  P2OUT = pin6;
          }
          if(min==53)
          {
        	  P1OUT = pin1 + pin3;
        	  P2OUT = pin5 + pin6;
          }
          if(min==54)
          {
        	  P1OUT = pin1 + pin3;
        	  P2OUT = pin7;
          }
          if(min==55)
          {
        	  P1OUT = pin1 + pin3;
        	  P2OUT = pin5 + pin7;
          }
          if(min==56)
          {
        	  P1OUT = pin1 + pin3;
        	  P2OUT = pin6 + pin7;
          }
          if(min==57)
          {
        	  P1OUT = pin1 + pin3;
        	  P2OUT = pin5 + pin6 + pin7;
          }
          if(min==58)
          {
        	  P1OUT = pin1 + pin3;
        	  P2OUT = pin8;
          }
          if(min==59)
          {
        	  P1OUT = pin1 + pin3;
        	  P2OUT = pin5 + pin8;
          }

          if(min==60)
          {
        	  P1OUT = 0x00;
        	  P2OUT = 0x00;
          }







    }
   // return 0;


}
