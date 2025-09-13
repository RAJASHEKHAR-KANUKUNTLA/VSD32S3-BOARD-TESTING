# VSD32S3-BOARD-TESTING
The VSD32S3 is a development board using THEJAS32 SoC, powered by VEGA ET1031 from C-DAC’s VEGA Processor family., RV32IM RISC-V processor at its core.

# Making an Blink led program - Tested 

Note: Low level Triggring 
``` c
// Blink LEDs on pins 16 and 19

int led1 = 16;
int led2 = 19;

void setup() {
  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
}

void loop() {
  // Turn both ON
  digitalWrite(led1, LOW);
  digitalWrite(led2, HIGH);
  delay(500);

  // Turn both OFF
  digitalWrite(led1, HIGH);
  digitalWrite(led2, LOW);
  
  delay(500);
}

```

# Bluetooth Control Led

connect bluetooth on UART-2
``` c
#include <UARTClass.h>

UARTClass MyBlue(2); // UART1: RX2/TX2
int LED_PIN = 17;

void setup() {
  Serial.begin(115200);
  MyBlue.begin(9600); // HC-05 default baud
  pinMode(LED_PIN, OUTPUT);
  digitalWrite(LED_PIN, LOW);
  Serial.println("Bluetooth LED Control Ready");
}

void loop() {
  if (MyBlue.available()) {
    String cmd = "";
    char c;
    while (MyBlue.available()) {
      c = (char)MyBlue.read();
      if (c == '\n') break;
      cmd += c;
    }
    cmd.trim();
    Serial.print("Received: ");
    Serial.println(cmd);

    if (cmd == "O") {
      digitalWrite(LED_PIN, HIGH);
      MyBlue.println("LED OFF");
    } else if (cmd == "F") {
      digitalWrite(LED_PIN, LOW);
      MyBlue.println("LED ON");
    } else {
      MyBlue.println("Invalid Command");
    }
  }
}

```
