#include <LiquidCrystal.h>

const int LED_ROJO = 9;                 
const int LED_VERDE = 8;                
const int BOTON = 10;                    
int val = 0;                            
int old_val = 0;                        
bool mostrarDireccion = false;          

LiquidCrystal lcd(2, 3, 7, 6, 5, 4);  

void setup() {
  pinMode(LED_ROJO, OUTPUT);   
  pinMode(LED_VERDE, OUTPUT);  
  pinMode(BOTON, INPUT);       
  lcd.begin(16, 2);            
  Serial.begin(9600);          
}

void loop() {
  // 🔄 Detectar cambio de estado del botón (de LOW a HIGH)
  val = digitalRead(BOTON);
  if (val == LOW && old_val == HIGH) {
    mostrarDireccion = true;

    Serial.println("Desconectado");
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Direccion 1");
    lcd.setCursor(0, 1);
    lcd.print("Direccion 2");

    digitalWrite(LED_ROJO, HIGH);
    digitalWrite(LED_VERDE, LOW);
    delay(200); // Anti-rebote
  }
  old_val = val;

  if (mostrarDireccion) {
    for (int pos = 16; pos >= -10; pos--) {
      if (!mostrarDireccion) break;

      lcd.clear();
      lcd.setCursor(pos, 0);
      lcd.print("Direccion 1");
      lcd.setCursor(pos, 1);
      lcd.print("Direccion 2");
      delay(500);

      if (Serial.available()) {
        char comando = Serial.read();

        if (comando == 'G') {
          Serial.println("Conectado");
          mostrarDireccion = false;

          lcd.clear();
          lcd.setCursor(5, 0);
          lcd.print("...");
          lcd.setCursor(5, 1);
          lcd.print("...");

          digitalWrite(LED_ROJO, LOW);
          digitalWrite(LED_VERDE, HIGH);
        }
        // Ya no se necesita que 'R' vuelva a reactivar esto, porque ya está activo
      }
    }
  } else {
    if (Serial.available()) {
      char comando = Serial.read();

      if (comando == 'G') {
        Serial.println("Conectado");
        mostrarDireccion = false;

        lcd.clear();
        lcd.setCursor(5, 0);
        lcd.print("...");
        lcd.setCursor(5, 1);
        lcd.print("...");

        digitalWrite(LED_ROJO, LOW);
        digitalWrite(LED_VERDE, HIGH);
      }

      else if (comando == 'R') {
        Serial.println("Desconectado");
        mostrarDireccion = true;

        lcd.clear();
        lcd.setCursor(0, 0);
        lcd.print("Direccion 1");
        lcd.setCursor(0, 1);
        lcd.print("Direccion 2");

        digitalWrite(LED_ROJO, HIGH);
        digitalWrite(LED_VERDE, LOW);
      }
    }
  }
}

