LED-digital-clock-7-segments-display
====================================

MSP430 code for minutes and hours
#include<msp430g2432.h>

#define pin1 BIT0
#define pin2 BIT1
#define pin3 BIT2
#define pin4 BIT3
#define pin5 BIT0
#define pin6 BIT1
#define pin7 BIT2
#define pin8 BIT4

char fracsec = 0; // local variable which counts up fractions of seconds
// based on the ticks from the interrupt
int sec = 0, min = 0, hour = 11;
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
//P1OUT = 0x00;
//P2OUT = 0x00;
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
	  ++hour;
	  min = 0; // reset the min counter
      }
if (hour == 24) // (1) increment hour - (2) is hour == 60
     {

     hour = 0; // reset the hour counter

     }


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
    	P1OUT = pin1;
    	P2OUT = pin5;

counter();
    while(1)
    {

    	if(hour==1)
    	      {
    		 P2OUT = pin5;
    	      }
    	 if(hour==2)
    	      {
    		 P2OUT = pin6;
    	      }
    	 if(hour==3)
    	       {
    		 P2OUT = pin5 + pin6;
    	       }
    	 if(hour==4)
    	 {
    		 P2OUT = pin7;

    	 }
    	 if(hour==5)
    	 {
    		 P2OUT = pin5 + pin7;
    	 }
    	  if(hour==6)
    	  {
    		  P2OUT= pin6 + pin7;
    	  }
    	  if(hour==7)
    	  {
    		  P2OUT = pin5 + pin6 + pin7;
    	  }
    	  if(hour==8)
    	  {
    		  P2OUT = pin8;
    	  }
    	  if(hour==9)
    	  {
    		  P2OUT = pin5 + pin8;
    	  }
    	  if(hour==10)
    	  {
    		  P1OUT = pin1;
    		  P2OUT = 0x00;

    	  }
    	  if(hour==11)
    	  {
    		  P1OUT = pin1;
    		  P2OUT = pin5;
    	  }
    	  if(hour==12)
    	  {
    		  P1OUT = pin1;
    		  P2OUT = pin6;
    	  }
    	  if(hour==13)
    	  {
    		  P1OUT = pin1;
    		  P2OUT = pin5 + pin6;
    	  }
    	  if(hour==14)
    	  {
    		  P1OUT = pin1;
    		  P2OUT = pin7;
    	  }
    	  if(hour==15)
    	  {
    		  P1OUT = pin1;
    		  P2OUT = pin5 + pin7;
    	  }
    	  if(hour==16)
    	  {
    		  P1OUT = pin1;
    		  P2OUT = pin6 + pin7;
    	  }
    	  if(hour==17)
    	  {
    		  P1OUT = pin1;
    		  P2OUT = pin5 + pin6 + pin7;
    	  }
    	  if(hour==18)
    	  {
    		  P1OUT = pin1;
    		  P2OUT = pin8;
    	  }
    	  if(hour==19)
    	  {
    		  P1OUT = pin1;
    		  P2OUT = pin5 + pin8;
    	  }
    	  if(hour==20)
    	  {
    		  P1OUT = pin2;
    		  P2OUT = 0x00;
    	  }
    	  if(hour==21)
    	    {
    	  	  P1OUT = pin2;
    	  	  P2OUT = pin5;
    	    }
    	    if(hour==22)
    	    {
    	  	  P1OUT = pin2;
    	  	  P2OUT = pin6;
    	    }
    	    if(hour==23)
    	    {
    	  	  P1OUT = pin2;
    	  	  P2OUT = pin5 + pin6;
    	    }
    	    if(hour==24)
    	    {
    	  	  P1OUT = pin2;
    	  	  P2OUT = pin7;
    	    }

    }























}
