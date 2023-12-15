NO.04
=====
#include <LiquidCrystal.h><br>
LiquidCrystal lcd(8, 9, 4, 5, 6, 7);<br>
char KeyValue[]={'1','2','3','4','5','6','7','8','9','0'};<br>
byte Row=0, Col=0;<br>
void setup() {<br>
  pinMode(10, INPUT); //R1: S1,S2,S3,S4 (1,2,3,A)  <br>                          
  pinMode(11, INPUT_PULLUP); //R2: S5,S6,S7,S8 (4,5,6,B) <br>
  pinMode(12, INPUT_PULLUP); //R3: S9, S10, S11,S12 (7,8,9,C)<br>
  pinMode(13, INPUT_PULLUP); //R4: (*,0,#,D)<br>
  pinMode(A0, OUTPUT); //A1, C1: S1,S5,S9 (1,4,7,*)<br>
  pinMode(A1, OUTPUT); //A2, C2: S2,S6,S10 (2,5,8,0)<br>
  pinMode(A2, OUTPUT); //A3, C3: S3,S7,S11 (3,6,9,#)<br>
  pinMode(A3, OUTPUT); //A4, C4, S4,S8,S12 (*,0, #,D)<br>
  //Pin left to right :R1 R2 R3 R4 C1 C2 C3 C4<br>
  digitalWrite(A0,HIGH);<br>
  digitalWrite(A1,HIGH);<br>
  digitalWrite(A2,HIGH);<br>
  digitalWrite(A3,HIGH);<br>
  lcd.begin(16, 2);              // start the library<br>
  lcd.setCursor(0,0);<br>
  for(int i=0; i<3;i++)<br>
  {<br>
    lcd.print("Key Martrix Test");<br>
    delay(1000);<br>
    lcd.clear();<br>
    delay(400);<br>
  }<br>
} <br>
void loop() {<br>
  // put your main code here, to run repeatedly:<br>
  static int keypressedcount=0;<br>
  byte keyindex=0;<br>
  //if key is pressed in the first round scan, <br>
  //then call keyscan() again to check if the key pressed in first round is actually pressed <br>
  if(keyscan()==true) <br>
  {<br>
    keyindex=(Row-1)*4+Col;<br>
    delay(5);<br>
    if ((keyscan()==true) && (keyindex=(Row-1)*4+Col))<br>
    {<br>
      lcd.clear();<br>
      lcd.setCursor(0,0);<br>
      lcd.print("Row=");lcd.print(Row);<br>
      lcd.print(",Col=");lcd.print(Col);<br>
      if(keyindex<=9){<br>
           lcd.setCursor(0,1);<br>
           lcd.print(KeyValue[keyindex-1]);<br>
        }else if(keyindex==10){<br>
            lcd.setCursor(0,1);<br>
            lcd.print(String(KeyValue[0])+String(KeyValue[9]));<br>
          }else if(keyindex==11){<br>
            lcd.setCursor(0,1);<br>
            lcd.print(String(KeyValue[0])+String(KeyValue[0]));<br>
           }else if(keyindex==12){<br>
              lcd.setCursor(0,1);<br>
            lcd.print(String(KeyValue[0])+String(KeyValue[1]));<br>
           }else if(keyindex==13){<br>
              lcd.setCursor(0,1);<br>
              lcd.print(String(KeyValue[0])+String(KeyValue[2]));<br>
              }else if(keyindex==14){<br>
              lcd.setCursor(0,1);<br>
              lcd.print(String(KeyValue[0])+String(KeyValue[3]));<br>
              }else if(keyindex==15){<br>
              lcd.setCursor(0,1);<br>
              lcd.print(String(KeyValue[0])+String(KeyValue[4]));<br>
              }else if(keyindex==16){<br>
              lcd.setCursor(0,1);<br>
              lcd.print(String(KeyValue[0])+String(KeyValue[5]));<br>
              }<br>
      digitalWrite(A0,LOW);<br>
      digitalWrite(A1,LOW);<br>
      digitalWrite(A2,LOW);<br>
      digitalWrite(A3,LOW);<br>
      delayMicroseconds(100);<br>
     while( (digitalRead(10)==LOW) || (digitalRead(11)==LOW))<br>
        ;  <br>
    }<br>
  } <br>
}<br>
bool keyscan( )<br>
{<br>
  Row=0;Col=0;<br>
  bool keypressed = false;<br>
  //scan col1<br>
  digitalWrite(A0, LOW);<br>
  digitalWrite(A1, HIGH);<br>
  digitalWrite(A2, HIGH);<br>
  digitalWrite(A3, HIGH);<br>
  delayMicroseconds(100);<br>
  //Read keys in row.1<br>
  if(digitalRead(10)==LOW)<br>
  {<br>
      digitalWrite(A0, HIGH);<br>
      Col=1;Row=1;<br>
      keypressed = true;<br>
      return(keypressed);<br>
  }<br>
  //Read keys in row.2<br>
  if(digitalRead(11)==LOW)<br>
  {<br>
      digitalWrite(A0, HIGH);<br>
      Col=1;Row=2;<br>
      keypressed = true;<br>
      return(keypressed);<br>
  }<br>
  //Read keys in row.3<br>
  if(digitalRead(12)==LOW)<br>
  {<br>
      digitalWrite(A0, HIGH);<br>
      Col=1;Row=3;<br>
      keypressed = true;<br>
      return(keypressed);<br>
  }<br>
  //Read keys in row.4<br>
  if(digitalRead(13)==LOW)<br>
  {<br>
       digitalWrite(A0, HIGH);<br>
      Col=1;Row=4;<br>
      keypressed = true;<br>
      return(keypressed);<br>
  }<br>
  //scan col 2<br>  
  digitalWrite(A0, HIGH);<br>
  digitalWrite(A1, LOW);<br>
  digitalWrite(A2, HIGH);<br>
  digitalWrite(A3, HIGH);<br>
  delayMicroseconds(100);<br>
  //Read keys in row.1<br>
  if(digitalRead(10)==LOW)<br>
  {<br>
      digitalWrite(A1, HIGH);<br>
      Col=2;Row=1;<br>
      keypressed = true;<br>
      return(keypressed);<br>
  }<br>
    //Read keys in row.2<br>
  if(digitalRead(11)==LOW)<br>
  {<br>
      digitalWrite(A1, HIGH);<br>
      Col=2;Row=2;<br>
      keypressed = true;<br>
      return(keypressed);<br>
  }<br>
  //Read keys in row.3<br>
  if(digitalRead(12)==LOW)<br>
  {<br>
      digitalWrite(A1, HIGH);<br>
      Col=2;Row=3;<br>
      keypressed = true;<br>
      return(keypressed);<br>
  }<br>
  //Read keys in row.4<br>
  if(digitalRead(13)==LOW)<br>
  {<br>
      digitalWrite(A1, HIGH);<br>
      Col=2;Row=4;<br>
      keypressed = true;<br>
      lcd.print(String(KeyValue[0]) + String(KeyValue[4]));<br>
      return(keypressed);<br>
  }<br>
  //scan col 3 <br>  
  digitalWrite(A0, HIGH);<br>
  digitalWrite(A1, HIGH);<br>
  digitalWrite(A2, LOW);<br>
  digitalWrite(A3, HIGH);<br>
  delayMicroseconds(100);<br>
  //Read keys in row.1<br>
  if(digitalRead(10)==LOW)<br>
  {<br>
      digitalWrite(A2, HIGH);<br>
      Col=3;Row=1;<br>
      keypressed = true;<br>
      return(keypressed);<br>
  }<br>
  //Read keys in row.2<br>
  if(digitalRead(11)==LOW)<br>
  {<br>
      digitalWrite(A2, HIGH);<br>
      Col=3;Row=2;<br>
      keypressed = true;<br>
      return(keypressed);<br>
  }  <br>
  //Read keys in row.3<br>
  if(digitalRead(12)==LOW)<br>
  {<br>
      digitalWrite(A2, HIGH);<br>
      Col=3;Row=3;<br>
      keypressed = true;<br>
      return(keypressed);<br>
  }<br>
  //Read keys in row.4<br>
  if(digitalRead(13)==LOW)<br>
  {<br>
      digitalWrite(A2, HIGH);<br>
      Col=3;Row=4;<br>
      keypressed = true;<br>
      return(keypressed);<br>
  }<br>
  
  //scan col 4<br>  
  digitalWrite(A0, HIGH);<br>
  digitalWrite(A1, HIGH);<br>
  digitalWrite(A2, HIGH);<br>
  digitalWrite(A3, LOW);<br>
  delayMicroseconds(100);<br>
  //Read keys in row.1<br>
  if(digitalRead(10)==LOW)<br>
  {<br>
      digitalWrite(A3, HIGH);<br>
      Col=4;Row=1;<br>
      keypressed = true;<br>
      return(keypressed);<br>
  }<br>
    //Read keys in row.2<br>
  if(digitalRead(11)==LOW)<br>
  {<br>
      digitalWrite(A3, HIGH);<br>
      Col=4;Row=2;<br>
      keypressed = true;<br>
      return(keypressed);<br>
  }<br>
  //Read keys in row.3<br>
  if(digitalRead(12)==LOW)<br>
  {<br>
      digitalWrite(A3, HIGH);<br>
      Col=4;Row=3;<br>
      keypressed = true;<br>
      return(keypressed);<br>
  }<br>
  //Read keys in row.4<br>
  if(digitalRead(13)==LOW)<br>
  {<br>
      digitalWrite(A3, HIGH);<br>
      Col=4;Row=4;<br>
      keypressed = true;<br>
      return(keypressed);<br>
  }<br>
  return(false);<br>
}<br>
*********************************************************************************************************
No.02
===
//Sample using LiquidCrystal library
#include <LiquidCrystal.h>
#define LATCH_DIO D15   
#define CLK_DIO D14
#define DATA_DIO 2
#define BUTTON1 BT1
#define BUTTON2 BT2
#define BUTTON3 BT3
#define BUTTON4 BT4
#define BUTTON_A1 A1
#define BUTTON_A2 A2
#define BUTTON_A3 A3
LiquidCrystal lcd(8, 9, 4, 5, 6, 7);
char KeyValue[]={'1','2','3','A','4','5','6','B','7','8','9','C','*','0','#','D'};
const byte SEGMENT_SELECT[] = {0xFE,0xFD,0xFB,0xF7};
byte Row=0, Col=0;
const byte SEGMENT_MAP[] = {0x3F,0x06,0x3C,0x4F,0x66,0x6D,0x7D,0x07,0X7F,0X6F,0X77,0X7C,0X39};

void setup() {
  pinMode(LATCH_DIO,OUTPUT);
  pinMode(CLK_DIO,OUTPUT);
  pinMode(DATA_DIO,OUTPUT);
  pinMode(10, INPUT); //R1: S1,S2,S3,S4 (1,2,3,A)                                   
  pinMode(11, INPUT_PULLUP); //R2: S5,S6,S7,S8 (4,5,6,B)
  pinMode(12, INPUT_PULLUP); //R3: S9, S10, S11,S12 (7,8,9,C)
  pinMode(13, INPUT_PULLUP); //R4: (*,0,#,D)
  pinMode(A0, OUTPUT); //A1, C1: S1,S5,S9 (1,4,7,*)
  pinMode(A1, OUTPUT); //A2, C2: S2,S6,S10 (2,5,8,0)
  pinMode(A2, OUTPUT); //A3, C3: S3,S7,S11 (3,6,9,#)
  pinMode(A3, OUTPUT); //A4, C4, S4,S8,S12 (*,0, #,D)

  digitalWrite(A0,HIGH);
  digitalWrite(A1,HIGH);
  digitalWrite(A2,HIGH);
  digitalWrite(A3,HIGH);
  lcd.begin(16, 2);              // start the library
  lcd.setCursor(0,0);
  for(int i=0; i<3;i++)
  {
    lcd.print("Key Martrix Test");
    delay(1000);
    lcd.clear();
    delay(400);
  }
} 

void loop() {
  // put your main code here, to run repeatedly:
  static int keypressedcount=0;
  byte keyindex=0;
  //if key is pressed in the first round scan, 
  //then call keyscan() again to check if the key pressed in first round is actually pressed 
  if(keyscan()==true) 
  {
    keyindex=(Row-1)*4+Col;
    delay(5);
    if ((keyscan()==true) && (keyindex=(Row-1)*4+Col))
    {
      lcd.clear();
      lcd.setCursor(0,0);
      lcd.print("Row=");lcd.print(Row);
      lcd.print(",Col=");lcd.print(Col);
      lcd.setCursor(0,1);
      lcd.print(KeyValue[keyindex-1]);
      digitalWrite(A0,LOW);
      digitalWrite(A1,LOW);
      digitalWrite(A2,LOW);
      digitalWrite(A3,LOW);
      delayMicroseconds(100);
     while( (digitalRead(10)==LOW) || (digitalRead(11)==LOW))
        ;  
    }
  }
  for(int i=3;i>=0;i--){
    {
      WriteNumberToSegment(i , 8);
    }
    delay(500);
  }
}

bool keyscan( )
{
  Row=0;Col=0;
  bool keypressed = false;
  //scan col1
  digitalWrite(A0, LOW);
  digitalWrite(A1, HIGH);
  digitalWrite(A2, HIGH);
  digitalWrite(A3, HIGH);
  delayMicroseconds(100);
  //Read keys in row.1
  if(digitalRead(10)==LOW)
  {
      digitalWrite(A0, HIGH);
      Col=1;Row=1;
      {
      WriteNumberToSegment(0 , 6);
      }
      keypressed = true;
      return(keypressed);
  }
  digitalWrite(A0, HIGH);
  digitalWrite(A1, LOW);
  digitalWrite(A2, HIGH);
  digitalWrite(A3, HIGH);
  delayMicroseconds(100);
  //Read keys in row.1
  if(digitalRead(10)==LOW)
  {
      digitalWrite(A1, HIGH);
      Col=2;Row=1;
      {
      WriteNumberToSegment(1 , 5);
      }  
      keypressed = true;
      return(keypressed);
  }
 //scan col 3  
  digitalWrite(A0, HIGH);
  digitalWrite(A1, HIGH);
  digitalWrite(A2, LOW);
  digitalWrite(A3, HIGH);
  delayMicroseconds(100);
  //Read keys in row.1
  if(digitalRead(10)==LOW)
  {
      digitalWrite(A2, HIGH);
      Col=3;Row=1;
      {
      WriteNumberToSegment(2 ,3);
      } 
      keypressed = true;
      return(keypressed);
  }  
  //scan col 4  
  digitalWrite(A0, HIGH);
  digitalWrite(A1, HIGH);
  digitalWrite(A2, HIGH);
  digitalWrite(A3, LOW);
  delayMicroseconds(100);
  //Read keys in row.1
  if(digitalRead(10)==LOW)
  {
      digitalWrite(A3, HIGH);
      Col=4;Row=1;
      {
      WriteNumberToSegment(3 , 3);
      } 
      keypressed = true;
      return(keypressed);
  }
  return(false);
}
void WriteNumberToSegment(byte Segment, byte Value)
{
digitalWrite(LATCH_DIO,LOW);
shiftOut(DATA_DIO, CLK_DIO, MSBFIRST, SEGMENT_MAP[Value]);
shiftOut(DATA_DIO, CLK_DIO, MSBFIRST, SEGMENT_SELECT[Segment] );
digitalWrite(LATCH_DIO,HIGH);
}
******************************************************************************************
No.03
=====
#include <LiquidCrystal.h>

LiquidCrystal lcd(8, 9, 4, 5, 6, 7);

void setup() {
  pinMode(BT1, INPUT);
  pinMode(BT2, INPUT);
  pinMode(BT3, INPUT);
  pinMode(BT4, INPUT);

}
int buttonState1,buttonState2,buttonState3,buttonState4 = 0;                                                 
int delay_number = 100;

void loop() {
  lcd.begin(16, 2);
  lcd.setCursor(0, 1);
  lcd.print("Andes Hello");

}
*****************************************************************************************
N.06
=====
int speakerPin = D3;
// 依照簡譜的順序，填入代表的音符，空白代表休止符
char notes[] = "ccggaagffeeddc ";
// 決定每個音階的拍子，注意這邊用 unsigned long 所以拍子只能是正整數
unsigned long beats[] = {1,1,1,1,1,1,2,1,1,1,1,1,1,2,4};
// 利用 sizeof()，算出總共要多少音符
int length = sizeof(notes);
// 決定一拍多長，這邊一拍 300 ms
int tempo = 300;

void setup() {
  pinMode(speakerPin, OUTPUT);
}

void loop() {
  // 利用 for 來播放我們設定的歌曲，一個音一個音撥放
  for (int i = 0; i < length; i++) {
 // 如果是空白的話，不撥放音樂
    if (notes[i] == ' ') {
      delay(beats[i] * tempo); // rest
    } else {
  // 呼叫 palyNote() 這個 function，將音符轉換成訊號讓蜂鳴器發聲
      playNote(speakerPin,notes[i], beats[i] * tempo);
    }
    // 每個音符之間的間隔，這邊設定的長短會有連音 or 段音的效果
    delay(tempo/10);
  }
}

void playNote(int OutputPin, char note, unsigned long duration) {
   // 音符字元與對應的頻率由兩個矩陣表示
  char names[] = { 'c', 'd', 'e', 'f', 'g', 'a', 'b', 'C' };
  int tones[] = { 261, 294, 330, 349, 392, 440, 494, 523 };
  // 播放音符對應的頻率
  for (int i = 0; i < 8; i++) {
    if (names[i] == note) {
      tone(OutputPin,tones[i], duration);
  //下方的 delay() 及 noTone ()，測試過後一定要有這兩行，整體的撥放出來的東西才不會亂掉，可能是因為 Arduino 送出tone () 頻率後會馬上接著執行下個指令，不會等聲音播完，導致撥出的聲音混合而亂掉
      delay(duration);
      noTone(OutputPin);
    }
  }
}
-------------------------------------------------------------------------
No.05
============
#include <LiquidCrystal.h>
#include <Wire.h>
LiquidCrystal lcd(8, 9, 4, 5, 6, 7);

void setup() {
  pinMode(BT1, INPUT);
  pinMode(BT2, INPUT);
  pinMode(BT3, INPUT);
}
int buttonState1,buttonState2,buttonState3,buttonState4 = 0;                                                 
int delay_number = 100;
int year=2020,month=12,d=25,h=12,m=59,s=55;
void loop() {
  lcd.clear();
  lcd.begin(16, 2);
  lcd.setCursor(0,0);
  lcd.print(year);
  lcd.print("/");
  lcd.print(month);
  lcd.print("/");
  lcd.print(d);
  lcd.setCursor(0,1);
  lcd.print(h);
  lcd.print(":");
  lcd.print(m);
  lcd.print(":");
  lcd.print(s);
  delay(1000);
  if(s==59){
    s=0;
    if(m==59){
      m=0;
      if(h==23){
        h=0;
        d++;
      }else
        h++;
      }else
        m++;
      }else 
        s++;
}
