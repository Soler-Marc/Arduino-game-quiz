    int resposta[7] = {0, 0,1,1,0,0,1};
    String pregunta[7] = {"LEDs usually tolerate up to 20mA", "Digital binary signals have two possible states: HIGH and LOW",

    "pinMode is declarated at loop()","A photoresistor is a type of resistor whose resistance increases when the intensity of light increases ",

    "A potentiometer is a simple knob that provides a variable resistance","Motion range of servos are from 0º to 180º", "Arduino UNO outputs operate at 4V"};

     //we create a string with some questions for our quiz



    // digital pin 2 has a pushbutton attached to it. Give it a name:

    int pushButtonG = 4;

    int pushButtonR = 2;//we declare the pins of the pushbuttons

    int ledG = 10;

    int ledR = 8;//we declare the pins of the LEDs

    int rnd = 0;

    int resultat;

    int contadorpregunta = 1;

    int contador = 0;//number of answers correct 

    // the setup routine runs once when you press reset:
    void setup() {

    // initialize serial communication at 9600 bits per second:
  
    Serial.begin(9600);
  
     // make the pushbutton's pin an input:
  
     pinMode(pushButtonG, INPUT);
  
    pinMode(pushButtonR, INPUT);//declare pushbuttons as an input
  
    pinMode(ledG, OUTPUT);
    
    pinMode(ledR, OUTPUT);//declare pushbuttons as an output
  
    }

    // the loop routine runs over and over again forever:

    void loop() {

    // read the input pin:


    Serial.print("QÜESTION ");Serial.print(contadorpregunta); Serial.println(":");
  
    Serial.println(pregunta[rnd]);//start with the question + witch number of question is it.
  
    int buttonStateG = HIGH;
  
    int buttonStateR = HIGH; //we check our pushbutton with DigitalRead and then we declare the initial state.

    while (buttonStateG == HIGH && buttonStateR == HIGH) {
  
    buttonStateG = digitalRead(pushButtonG);
    
    buttonStateR = digitalRead(pushButtonR);//if our pushbuttons are high=read our funtion.
    
   }

    int resp = -1;
  
    if (buttonStateG == LOW) {
  
    resp = 0;
    } else {
  
    resp = 1; //if we push TRUE button answer is correct else incorrect.
   }

    while (buttonStateG == LOW || buttonStateR == LOW) {
  
    buttonStateG = digitalRead(pushButtonG);
    buttonStateR = digitalRead(pushButtonR); //if our pushbuttons are low=read our funtion.
    }

    if (resp == resposta[rnd]) {
  
    Serial.println("CORRECT!");
        digitalWrite(ledR, HIGH);
    delay (500);
    digitalWrite(ledR, LOW);//if answer is correct green light.
    contador++;


     } else {
  
    Serial.println("INCORRECT!");
    digitalWrite(ledG, HIGH);
    delay (500);
    digitalWrite(ledG, LOW);//if answers is incorrect red light

    }
    rnd = rnd + 1; //next question
  
    contadorpregunta = contadorpregunta +1;//next numer of question
  
    if (rnd >= 7) {
  
    Serial.println("END OF THE GAME!");
    Serial.print("Total points: ");//final text
    Serial.println(contador);
    
    contador = 0;//restart
    rnd = 0;//restart
    contadorpregunta = 1;//restart
   

      }

    }
