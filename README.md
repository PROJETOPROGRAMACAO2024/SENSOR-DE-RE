#define TRIGGER_PIN 3 // Pino de gatilho do sensor de distância
#define ECHO_PIN 2     // Pino de eco do sensor de distância

#define LED1_PIN 13     // Pinos dos LEDs
#define LED2_PIN 12
#define LED3_PIN 11
#define LED4_PIN 10
#define LED5_PIN 9
#define LED6_PIN 8

#define BUZZER_PIN 7  // Pino do buzzer (piezo)

void setup() {
  pinMode(TRIGGER_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  
  pinMode(LED1_PIN, OUTPUT);
  pinMode(LED2_PIN, OUTPUT);
  pinMode(LED3_PIN, OUTPUT);
  pinMode(LED4_PIN, OUTPUT);
  pinMode(LED5_PIN, OUTPUT);
  pinMode(LED6_PIN, OUTPUT);
  
  pinMode(BUZZER_PIN, OUTPUT);
}

void loop() {
  // Aciona o pulso de gatilho
  digitalWrite(TRIGGER_PIN, LOW);
  delayMicroseconds(10);
  digitalWrite(TRIGGER_PIN, HIGH);
  delayMicroseconds(2);
  digitalWrite(TRIGGER_PIN, LOW);
  
  // Mede a duração do eco
  long duration = pulseIn(ECHO_PIN, HIGH);
  
  // Calcula a distância em centímetros
  long distance = (duration / 2) / 29.1;
  
  // Ativa LEDs e o buzzer com base na distância medida
  if (distance < 40) {
    digitalWrite(LED1_PIN, HIGH);
    tone(BUZZER_PIN, 1000);
  } else if (distance < 80) {
    digitalWrite(LED2_PIN, HIGH);
    tone(BUZZER_PIN, 800);
  } else if (distance < 114) {
    digitalWrite(LED3_PIN, HIGH);
    tone(BUZZER_PIN, 600);
  } else if (distance < 170) {
    digitalWrite(LED4_PIN, HIGH);
  } else if (distance <250 ) {
    digitalWrite(LED5_PIN, HIGH);
  } else if (distance <334.2 ) {
    digitalWrite(LED6_PIN, HIGH);
    noTone(BUZZER_PIN);
  } else {
    digitalWrite(LED6_PIN, LOW);
    noTone(BUZZER_PIN);
  }
  
  // Espera um curto período antes de fazer a próxima medição
  delay(100);
  
  // Desliga todos os LEDs e o buzzer para a próxima medição
  digitalWrite(LED1_PIN, LOW);
  digitalWrite(LED2_PIN, LOW);
  digitalWrite(LED3_PIN, LOW);
  digitalWrite(LED4_PIN, LOW);
  digitalWrite(LED5_PIN, LOW);
  digitalWrite(LED6_PIN, LOW);
  noTone(BUZZER_PIN);
}
