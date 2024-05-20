#include <SoftwareSerial.h>
const int motor1Pin1 = 2; // Pin 1 del Motor 1
const int motor1Pin2 = 3; // Pin 2 del Motor 1
const int motor2Pin1 = 4; // Pin 1 del Motor 2
const int motor2Pin2 = 7; // Pin 2 del Motor 2
int enA=10;//Pin PWM Motor A
int enB=11;//Pin PWM Motor B

SoftwareSerial bt(9,8);//Creación de un puerto receptor-transmisor bt(RX,TX)
void setup() {

  bt.begin(9600);//Iniciamos el puerto bt
  Serial.begin(9600);//Inicio del puerto serie
 
  pinMode(motor1Pin1, OUTPUT);
  pinMode(motor1Pin2, OUTPUT);
  pinMode(motor2Pin1, OUTPUT);
  pinMode(motor2Pin2, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
  if(bt.available() >0){
    char character=bt.read();
    if (character=='U'){
      Serial.println("ADELANTE");
      moverAdelante();
    }
    if (character=='D'){
       Serial.println("ATRAS");
      moverAtras();
    }
    if (character=='R'){
       Serial.println("DERECHA"); 
       moverDerecha();     

    }
    if (character=='L'){
       Serial.println("IZQUIERDA");
       moverIzquierda();
    }
    if (character=='S'){
      detenerMotores();
    }

  }
}
void moverAdelante() {
  // Motor 1 hacia adelante
  digitalWrite(motor1Pin1, HIGH);
  digitalWrite(motor1Pin2, LOW);
  analogWrite(enA,255);
  // Motor 2 hacia adelante
  digitalWrite(motor2Pin1, HIGH);
  digitalWrite(motor2Pin2, LOW);
    analogWrite(enB,255);

  
}

void moverAtras() {
  // Motor 1 hacia atrás
  digitalWrite(motor1Pin1, LOW);
  digitalWrite(motor1Pin2, HIGH);
  analogWrite(enA,255);
  // Motor 2 hacia atrás
  digitalWrite(motor2Pin1, LOW);
  digitalWrite(motor2Pin2, HIGH);
  analogWrite(enB,255);
}

void detenerMotores() {
  // Detener Motor 1
  digitalWrite(motor1Pin1, LOW);
  digitalWrite(motor1Pin2, LOW);
    analogWrite(enA,255);
  // Detener Motor 2
  digitalWrite(motor2Pin1, LOW);
  digitalWrite(motor2Pin2, LOW);
    analogWrite(enB,255);
}
void moverDerecha(){
  // Motor 1 hacia atrás
  digitalWrite(motor1Pin1, LOW);
  digitalWrite(motor1Pin2, HIGH);
    analogWrite(enA,255);
  // Motor 2 hacia adelante
  digitalWrite(motor2Pin1, HIGH);
  digitalWrite(motor2Pin2, LOW);
    analogWrite(enB,255);
}
void moverIzquierda(){
  // Motor 1 hacia adelante
  digitalWrite(motor1Pin1, HIGH);
  digitalWrite(motor1Pin2, LOW);
    analogWrite(enA,255);
  // Motor 2 hacia atrás
  digitalWrite(motor2Pin1, LOW);
  digitalWrite(motor2Pin2, HIGH);
    analogWrite(enB,255);
}
