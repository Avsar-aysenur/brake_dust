#include <PIC18F4520.h>

#define POT    PIN_A0
#define BUTTON PIN_B2
#define OPTO   PIN_C2
#define LED    PIN_D3

int16 analogBilgi ;

void main()
{
   setup_adc_ports(AN0);
   setup_adc(ADC_CLOCK_DIV_16);
   setup_timer_2(T2_DIV_BY_16,255,1);      //819 us overflow, 819 us interrupt

   setup_ccp1(CCP_PWM|CCP_SHUTDOWN_AC_L|CCP_SHUTDOWN_BD_L);
   
   set_tris_d(0x00);
   output_d(0x00);
   set_tris_c(0x00);
   output_c(0x00);
   set_tris_b(0b10000000);
   output_b(0x00);  
   
   while(TRUE)
   {
   
 set_adc_channel(0);  
 analogBilgi = read_adc();
    
   if(INPUT(BUTTON) == 1){
   set_pwm1_duty((int16) analogBilgi);
   output_high(LED);
  }
   else{
  set_pwm1_duty((int16) 0);
  output_low(LED);
   
  }
}}
