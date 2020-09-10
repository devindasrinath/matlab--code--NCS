 .. code-block:: c

     void Setup(){
	pinMode(27,OUTPUT);
	pinMode(34,INPUT);
     }
     void loop(){

      int buttonState = digitalRead(34);
      if(buttonState == LOW){
	digitalWrite(27, HIGH);
      }else{
	digitalWrite(27, LOW);
      }
     }
