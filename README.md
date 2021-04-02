# parksens-r-
mesafesensörü
const int trigger_pin = 12;
const int echo_pin = 13;
const int buzzer = 2;
const int mled = 3;  //pinlerimizi tanımladık
const int yled = 4;
const int sled = 5;
const int kled = 6;

int sure;
int mesafe;    //sure ve mesafe adlı değişkenler oluşturuyoruz

void setup() {
  pinMode(kled, OUTPUT);
  pinMode(sled, OUTPUT);  
  pinMode(yled, OUTPUT);   //ledlerimizi,buzzerımızı ve mesafe sensörümüzün pinlerinden trigpini çıkış olarak tanımladık
  pinMode(mled, OUTPUT);
  pinMode(buzzer, OUTPUT);
  pinMode(trigger_pin, OUTPUT);
  pinMode(echo_pin, INPUT); // mesafe sensörümüzün pinlerinden echopini giriş olarak tanımladık
  Serial.begin(9600); //serial haberleşme başlattık
}

void loop() {
  digitalWrite(trigger_pin, HIGH);
  delayMicroseconds(1000);         //trigpinin ölçüm yapabilmesi için her 1 saniyede bir dalga göndermesini sağlıyoruz             
  digitalWrite(trigger_pin, LOW);  
  sure = pulseIn(echo_pin, HIGH);
  mesafe = (sure / 2) / 28.5;//echopinden alınan dalganın gelme süresini cm'e çeviriyoruz

  if (mesafe <= 10)
  {
    digitalWrite(kled, HIGH);
    digitalWrite(buzzer, HIGH);
    delay(50);                 //mesafe 10 cm'e eşit veya az ise kırmızı led ve buzzera 50 milisaniye enerji ver ve 250 milisaniye  enerji kes
    digitalWrite(kled, LOW);
    digitalWrite(buzzer, LOW);
    delay(250);
  }

  else if (mesafe <= 25)
  {
    digitalWrite(sled, HIGH);
    digitalWrite(buzzer, HIGH);
    delay(50);                   //mesafe 25 cm'e eşit veya az ise sarı led ve buzzera 50 milisaniye enerji ver ve 500 milisaniye enerji kes
    digitalWrite(sled, LOW);
    digitalWrite(buzzer, LOW);
    delay(500);
  }

  else if (mesafe <= 50)
  {
    digitalWrite(yled, HIGH);
    digitalWrite(buzzer, HIGH);
    delay(50);               //mesafe 50 cm'e eşit veya az ise yeşil led ve buzzera 50 milisaniye enerji ver ve 75050 milisaniye enerji kes
    digitalWrite(yled, LOW);
    digitalWrite(buzzer, LOW);
    delay(750);
  }

  else
  {
    digitalWrite(mled, HIGH);
    delay(1000);               //mesafe bu değerlerden birisi değil ise her saniye başı mavi led'e enerji ver ve 1 saniye sonra enerji kes
    digitalWrite(mled, LOW);
    delay(1000);
  }
}

