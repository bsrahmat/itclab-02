# PWM Testing

PWM_Testing is a simple program for testing Pulse Width Modulation (PWM) of the iTCLab Kit. This PWM setting will later be used to increase and decrease the heat on the iTCLab heater.

Pulse Width Modulation (PWM) is a modulation technique that changes the pulse width with a constant frequency and amplitude value. PWM can be considered as the opposite of ADC (Analog to Digital Converter) which converts Analog signals to Digital, PWM is used to generate analog signals from Digital devices (iTCLab Kit).

The PWM signal will remain ON for a certain period of time and then stop or OFF for the rest of the period. What makes PWM special and more useful is that we can determine how long the ON condition should last by controlling the duty cycle of the PWM.
<br>
</br>

<p align="center">
  <img src="https://github.com/bsrahmat/itclab-01/blob/main/itclab01a.jpg" alt="" class="img-responsive" width="700">
</p>

## About these iTCLab kits :

iTCLab - Internet-Based Temperature Control Lab. Temperature control kit for feedback control applications with an ESP32 Microcontroller, LED, two heaters, and two temperature sensors. The heating power output is adjusted to maintain the desired temperature setpoint. Heat energy from the heater is transferred by conduction, convection, and radiation to the temperature sensor. Heat is also transferred from the device to the environment.

### More about iTCLab:

- It is inspired by <a href="https://apmonitor.com/pdc/index.php/Main/ArduinoTemperatureControl" target="_blank">The TCLab Product of Brigham Young University (BYU), one of the private campuses in Provo, Utah, United States of America.</a>
- Miniature Control System in a Pocket.
- Practical IoT Learning Package Tools.
- IoT programming Kits.
- IoT-Based Control System Practice Devices.
- It can be used to learn System Dynamics and Control Systems.
- It can be used to learn Arduino and Python programming.
- It can be used to learn AI and Machine Learning Programming.
- And others.

The fundamental difference between iTCLab and BYU's TCLab product is the replacement of the Arduino Uno microcontroller with the ESP32. By using the ESP32, iTCLab has the ability to connect to the Internet of Things (IoT).
<br>
</br>

## iTCLab Upper Temperature Limit Description:

The upper temperature limit of the iTCLab Kit is 60 degrees Celsius. Therefore, when experimenting with this Kit, this Upper Temperature Limit must not be exceeded. Violation of this provision could cause damage (burning) to the components.

Although the upper limit is 60 degrees Celsius, it is still sufficient for experimenting with this Kit. And it is sufficient to see the performance of a control method. For example, control using Proportional Integral and Derivative (PID). Or to see the effect of tuning the PID parameters using the Machine Learning method. An illustration of the capabilities of this iTCLab Kit can be seen from the illustration of the performance of the BYU TCLab, as seen in the following simulation.

<p align="center">
  <img src="https://github.com/bsrahmat/itclab-01/blob/main/pid_control.gif" alt="" class="img-responsive" width="700">
</p>

## Coding Upper Temperature Limit

It is necessary to set a limit so that the iTCLab Kit always operates in a safe area. It must not exceed the upper limit of 60 degrees Celsius. The following is an example of an Arduino program script that must be added every time you experiment with this Kit. In the Loop, it is added that if it reaches the specified upper limit (it can be lowered slightly, for example 55 degrees Celsius), then the heater must be turned off.

```
void loop() {
  // put your main code here, to run repeatedly:
  cektemp();
  if (cel > upper_temperature_limit){
    Q1off();
    ledon();
  }
  else {
    Q1on();
    ledoff();
  }
  if (cel1 > upper_temperature_limit){
    Q2off();
    ledon();
  }
  else {
    Q2on();
    ledoff();
  }
  delay (100);
}

```
<br>
</br>

## PWM Testing Program

PWM_Testing is a simple program for testing Pulse Width Modulation (PWM) of the iTCLab Kit. This PWM setting will later be used to increase and decrease the heat on the iTCLab heater. In this simple PWM Testing program example, the result of the PWM setting is shown by turning on the LED from dim to bright, and from bright to dim. Repeatedly.
<br>
</br>

## Required Equipment:

- <a href="https://shopee.co.id/product/78709625/11589970517/" target="_blank">iTCLab Kit</a>

- <a href="https://github.com/bsrahmat/itclab-02/blob/main/PWM_Testing.ino" target="_blank">PWM_Testing.ino Program</a>

- <a href="https://github.com/bsrahmat/itclab-02/blob/main/PWM_Testing.pdf" target="_blank">PWM_Testing.pdf Tutorial</a>


### Another alternative is to download the tutorial:

- <a href="https://www.academia.edu/116155979" target="_blank">https://www.academia.edu/116155979</a>

- <a href="https://www.researchgate.net/publication/378904388" target="_blank">https://www.researchgate.net/publication/378904388</a>

<br>
</br>

### Here is the complete coding for PWM_Testing:

```
/*********************************************************************************
 * Program   : PWM_Testing
 * By        : Assoc. Prof. Dr. Basuki Rahmat, S.Si, MT, ITS-AI, et al
 * Pro. Team : i-ot.net, io-t.net
 * R. Group  : Intelligent Control, Robotics and Automation Systems Research Group
 * Univ.     : Universitas Pembangunan Nasional "Veteran" Jawa Timur
 * Country   : Indonesia
 *********************************************************************************/
 
// the number of the LED pin
const int ledPin = 26;

// setting PWM properties
const int freq = 5000;
const int ledChannel = 0;
const int resolution = 8;
 
void setup(){
  // configure LED PWM functionalitites
  ledcSetup(ledChannel, freq, resolution);
  
  // attach the channel to the GPIO to be controlled
  ledcAttachPin(ledPin, ledChannel);
}
 
void loop(){
  // increase the LED brightness
  for(int dutyCycle = 0; dutyCycle <= 255; dutyCycle++){   
    // changing the LED brightness with PWM
    ledcWrite(ledChannel, dutyCycle);
    delay(20);
  }

  // decrease the LED brightness
  for(int dutyCycle = 255; dutyCycle >= 0; dutyCycle--){
    // changing the LED brightness with PWM
    ledcWrite(ledChannel, dutyCycle);   
    delay(20);
  }
}


```

<br>
</br>

An example of the test results is shown in the following figure.


<p align="center">
  <img src="https://github.com/bsrahmat/itclab-02/blob/main/PWM2.jpg" alt="" class="img-responsive" width="700">
</p>

<br>
</br>

## An example of a publication related to this Kits:

<a href="https://www.igi-global.com/pdf.aspx?tid=319461&ptid=296384&ctid=4&oa=true&isxn=9781668456293" target="_blank">iTCLab Temperature Monitoring and Control System Based on PID and Internet of Things (IoT)</a>

<a href="https://www.academia.edu/102829350" target="_blank">Temperature Monitoring via the Internet of Things Using PID-iTCLab</a>

<a href="https://www.academia.edu/102829413" target="_blank">On/Off Temperature Monitoring and Control via the Internet of Things Using iTCLab Kit</a>

<a href="https://ieeexplore.ieee.org/document/10420130" target="_blank">iTCLab PID Control Tuning Using Deep Learning</a>
<br>
</br>

## Other publications by the researcher:

https://fitri.academia.edu/BasukiRahmat

https://www.researchgate.net/profile/Basuki-Rahmat-2

https://scholar.google.com/citations?user=BjCi4AgAAAAJ&hl=en
<br>
</br>

## Buy the iTCLab Kits at Shopee:

<p align="center">
<a href="https://shopee.co.id/product/78709625/11589970517" target="_blank"><img src="https://github.com/bsrahmat/itclab-01/blob/main/shopee_kit1.jpg" alt="" class="img-responsive" width="700">
</a>
</p>
<br>
</br>

## Other research by the IO-T.Net research team can be found at:

https://www.io-t.net/

<p align="center">
<a href="https://www.io-t.net/" target="_blank"><img src="https://github.com/bsrahmat/robot-bnu/blob/main/iot.png" alt="" class="img-responsive" width="500">
</a>
</p>

<br>
</br>

## Other research by the I-OT.Net research team can be found also at:

https://www.i-ot.net/

<p align="center">
<a href="https://www.i-ot.net/" target="_blank"><img src="https://github.com/bsrahmat/fuzzy-neural/blob/main/iot_logo.png" alt="" class="img-responsive" width="500">
</a>
</p>

