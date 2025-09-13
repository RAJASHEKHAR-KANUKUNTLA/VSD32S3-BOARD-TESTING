# VSD32S3-BOARD-TESTING
The VSD32S3 is a development board using THEJAS32 SoC, powered by VEGA ET1031 from C-DAC’s VEGA Processor family., RV32IM RISC-V processor at its core.

# Making an Blink led program - Tested 
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
