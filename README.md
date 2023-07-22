# Object_Counter
Object counter using IR sensors, OLED, and arduino uno


#include<LiquidCrystal.h>

LiquidCrystal lcd(2,3,4,5,6,7);

const int ir_input=8;

const int ir_output=9;

unsigned int count=0u;

bool ir_entry=LOW;

bool ir_exit=LOW;

bool add_count=LOW;

bool remove_count=LOW;

void setup() {

  // put your setup code here, to run once:
  
  pinMode(ir_input, INPUT);
  
  pinMode(ir_output,OUTPUT);
  
  lcd.begin(16,2);
  
  lcd.print("Object Counter");
  
  delay(1000);
  
}

void loop() {

  // put your main code here, to run repeatedly:
  
  ir_entry=digitalRead(ir_input);
  
  ir_exit=digitalRead(ir_output);
  
  if(ir_entry==1){
  
    if(add_count==LOW){
    
      add_count=HIGH;
      
      count=count+1u;
      
      lcd.clear();
      
      lcd.print("one object added");
      
      delay(200);
      
  }
  
  else{
  
      add_count=LOW;
      
      lcd.clear();
      
      lcd.print("waiting for next object");
      
      delay(100);
      
  }
  
  lcd.clear();
   
  lcd.print("Total objects");
  
  lcd.setCursor(3,2);
  
  lcd.print(count);
  
  delay(500);
  
  }
  
 if(ir_exit==HIGH)
 
 {
 
  if(remove_count==LOW and (count>0))
  
  {
  
    remove_count=HIGH;
    
    count=count-1u;
    
    lcd.clear();
    
    lcd.print("object removed");
    
    delay(200);
    
  }
  
  else
  
  {
  
    remove_count=LOW;
    
    lcd.clear();
    
    lcd.print("waiting for next object");
    
    delay(100);
    
  }
  
  lcd.clear();
  
  lcd.print("Total objects");
  
  lcd.setCursor(3,2);
  
  lcd.print(count);
  
  delay(500);
  
 }
 
}
