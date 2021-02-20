/*****************************************************************************************************
  * Microprocessors Assignment 2 PART B
  * Mechatronics 4.2 ,2021
  -> Least digit in Reg. No =2, from E022-01-0723/2017
  -> The traffic operates in four phases(1,2,3,4) with each phase controlling traffic and pedestrian flow
  -> The circuit also has a 7 segment led that shows the current phase
  -> Bidirectional leds have been used for pedestrian's signalling
  -> Traffic light module used in Proteus
*****************************************************************************************************/
#define F_CPU 16000000UL 
#include <avr/io.h> 
#include <util/delay.h>

void phase1();
void phase2();
void phase3();
void phase4();
void orange();

int main(void)
{
  /*****************************************************************************************************/
  //Setting pin modes as outputs
  /*****************************************************************************************************/
  DDRA=0XFF;
  DDRB=0XFF;
  DDRC=0XFF;
  DDRD=0XFF;
  
  while(1)
  {
    /*****************************************************************************************************
     * control the lights using the phases
     * we need to turn on the orange lights for the traffic lights before the transition(for 1 second)
     * we also need to set the pedestrian's lights to red to stop their movement
     * do this between the phases
    *****************************************************************************************************/
    phase1();
    orange();
    phase2();
    orange();
    phase3();
    orange();
    phase4();
  }
  return 0;
}

void phase1()
{
  /*****************************************************************************************************/
  // This enables vehicles in A to travel to F and those in E to travel to B
  // We therefore give greenlight for A and E and redlight for East and West roads.
  // We also give green on East & West pedestrian paths
  /*****************************************************************************************************/
  PORTA = 0b10100001;
  PORTB = 0b10100001;
  PORTC = 0b10100101;
  //PORTD = 0b00000101;
  PORTD = 0b00010101; //display 1
  _delay_ms(2000);
  /*
  PORTA |= (1<<PA0) | (1<<PA7); //turn NG on and PED1 to green
  PORTB |= (1<<PB0) | (1<<PB7); //turn SG on and PED2 to green
  PORTC |= (1<<PC5) | (1<<PC7); //turn PED5 and PED6 to green
  //we now set redlight on East and West roads and red on PEDs 3,4,7,8
  PORTA |= (1<<PA5); //turn ER on
  PORTB |= (1<<PB5); //turn WR on
  PORTC |= (1<<PC0) | (1<<PC2); //turn PEDs 3 and 4 red
  PORTD |= (1<<PD0) | (1<<PD2); //turn PEDs 7 and 8 red

  //we now wait for a delay of 2 sec
  _delay_ms(2000);
  //go to phase 2
  */
}

void phase2()
{
  /*****************************************************************************************************/
  // This enables vehicles in G to travel to D and those in C to travel to H
  // We therefore give greenlight for G and C and redlight for Nort and South roads.
  // We also give green on North & South pedestrian paths
  /*****************************************************************************************************/
  PORTA = 0b01001100;
  PORTB = 0b01001100;
  PORTC = 0b01011010;
  //PORTD = 0b00001010;
  PORTD = 0b00101010; //display 2
  _delay_ms(2000);
  /*
  PORTA |= (1<<PA3) | (1<<PA6); //turn EG on and PED1 to red
  PORTB |= (1<<PB3) | (1<<PB6); //turn WG on and PED2 to red
  PORTC |= (1<<PC1) | (1<<PC3); //turn PEDs 3,4 to green
  PORTD |= (1<<PD1) | (1<<PD3); //turn PEDs 7,8 to green
  //we now set redlight on North and South roads and red on PEDs 5,6
  PORTA |= (1<<PA2); //turn NR on
  PORTB |= (1<<PB2); //turn SR on
  PORTC |= (1<<PC4) | (1<<PC6); //turn PEDs 5 and 6 red

  //we now wait for a delay of 2 sec
  _delay_ms(2000);
  //go to phase 3
  */
}
void phase3()
{
  /*****************************************************************************************************/
  // This enables vehicles in A to travel to D and those in E to travel to H
  // Turn green on NG and SG
  // Turn red on WR and ER
  // PEDs 2,3,6,7 are greeen
  // PEDs 1,4,5,8 are red
  /*****************************************************************************************************/
  PORTA = 0b01100001;
  PORTB = 0b10100001;
  PORTC = 0b10010110;
  //PORTD = 0b00000110;
  PORTD = 0b00110110; //display3
  _delay_ms(2000);
  //go to phase 4
}
void phase4()
{
  /*****************************************************************************************************/
  // This enables vehicles in C to travel to F and those in G to travel to B
  // Turn green on EG and WG
  // Turn red on NR and SR
  // PEDs 1,4,5,8 are green
  // PEDs 2,3,6,7 are red
  /*****************************************************************************************************/
  PORTA = 0b10001100;
  PORTB = 0b01001100;
  PORTC = 0b01101001;
  //PORTD = 0b00001001;
  PORTD = 0b01001001; //display  4
  _delay_ms(2000);
  //go to phase 1
}
void orange()
{
  /*****************************************************************************************************
  * we need to turn on the orange lights for the traffic lights before the transition(for 1 second)
  * we also need to set the pedestrian's lights to red to stop their movement
  * do this between the phases
  *****************************************************************************************************/
  PORTA = 0b01010010;
  PORTB = 0b01010010;
  PORTC = 0b01010101;
  PORTD = 0b00000101;
  _delay_ms(1000);
}
