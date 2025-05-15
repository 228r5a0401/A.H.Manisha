#include <LiquidCrystal.h>
const int rs = 15, en = 14, d4 = 13, d5 = 12, d6 = 11, d7 = 10;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
UART Serial2(8, 9, NC, NC);//9rx 8tx
String data1="";
String data2="";
int temp=0;
void setup() 
{
  lcd.begin(16, 2);
  lcd.print("hello, world");
  Serial.begin(9600);
  Serial2.begin(9600);//9rx 8tx
}

void loop()
{
back:
 while(Serial2.available())
 {
   data1=Serial2.readString(); //PH:37.76, W: 0, L:  54, T:  61,
     lcd.clear();
  int len=data1.length();
  int i=0;lcd.clear();
  for(i=1;i<=len;i++)
  { 
   lcd.print(data1[i]);delay(1);
   if(i==15)
   lcd.setCursor(0,1);delay(1); 
  }
 temp=temp+1;
 if(temp==10)
 {
 int len=data1.length();
int i=0;
for(i=0;i<len;i++)
{
 if(data1[i]==' '  || data1[i]==',' || data1[i]==':')
 {
  data1[i]='_'; 
 }
}
  
Serial2.println(data1);delay(1);
lcd.clear();lcd.print("DATA UPLOADED.....");delay(1000);
temp=0;
data1.replace("","")
Serial.println(data1);
 }
 }
}
