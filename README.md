# arduino489

https://youtu.be/HOEv0LQjR9A<BR>
  
ESP8266+Wemos D1 mini+LoRa(SX1276)+DeepSleep

간만에 진행해보는 녹칸다의 LoRa시리즈이다!
이번편은 녹칸다가 최근에 새롭게 구입한 Wemos d1 mini보드에서 LoRa모듈은 sx1276이 정상적으로 작동되는지 확인하고 딥슬립(deepsleep)을 적용시켜 보도록 한다!

2대의 보드가 LoRa로 메시지를 주고받는데 센서가 달린 보드쪽에서 LoRa로 데이터를 전송한다음 deepsleep을 하면서 베터리 세이프를 하는 것이다!

여기서 센서가 달린 보드를 '노드'라고 하고 수집하는 보드를 '게이트웨이'라고 부르게 될 것인데 노드는 베터리가 달려있고 게이트웨이는 상시전원을 공급받는다는 가정을 하고 시작한다!

즉 센서값을 어딘가 설치되어 있는 보드가 업로드를 하는데 베터리가 달려있으므로 전기를 아껴써야 하는 개념이다!

그리고 기존 LoRa에서 하지 않았던 아래 내용도 같이 테스트 해보도록 한다!<BR>
1.txpower를 변경하는 기능을 확인해보고 소모전류를 측정하시오!<BR>
2.LoRa모듈 자체의 sleep기능을 확인해보고 소모전류를 측정하시오!<BR>
3.딥슬립일때와 아닐때의 소모전류의 차이를 확인하시오!<BR>
4.몇가지 센서를 준비해서 센서값을 전송시켜보시오!<BR>
(온습도,이산화탄소,미세먼지,DS18B20,조도센서 등등)<BR>
(녹칸다 마음대로)

(실제로한거)

*딥슬립이 적용된 보드에 프로그램을 현재 올리려면 아래 순서로 하시오!<BR>
1.RST와 D0에 연결된 선을 먼저 뽑는다<BR>
2.D3에 뭔가 연결되어있다면 일단 뽑는다!<BR>
3.프로그램 업로드를 한다!<BR>
4.(1)과(2)에서 뽑았던것을 다시 연결한다!

1.Wemos d1 mini보드에 sx1276모듈을 연결해서 게이트웨이와 노드로 구성된 2개의 보드가 양방향 통신이 되는지 확인하는 예제!

![489-1_bb](https://user-images.githubusercontent.com/106683637/171844332-cb5d450a-403c-4d90-97d7-2b5f26b3d696.jpg)
  
2.(코드는 1과 같음) 1에서 게이트웨이와 노드가 소모하는 전류의 양을 멀티미터로 측정해서 결과를 첨부하시오!(평소에는 85, 메시지전송할때 최대 120)

3.게이트웨이와 노드에서 보내는 tx파워를 20으로 올렸을때의 소모전류량을 측정하시오!(120ma에서 135ma까지 올라간것을 확인함)

4.LoRa라이브러리안에 sleep함수가 어떻게 작동되는지 확인하시오!(sleep을 걸면 5ma정도 절약이되더라/대신 수신이 안됨)

5.센서가 달려있는 노드를 적절한 타이밍에 deepsleep시키시오!(LoRa+wemos d1 mini+ deepsleep의 기본형태의 예제)(딥슬립일때 4.3ma/데이터전송할때 대략80~100ma)

![489-5_bb](https://user-images.githubusercontent.com/106683637/171844331-61387407-289d-49de-95bd-7bc18be66894.jpg)
  
6.노드에 온습도센서(DHT-11)을 연결해서 온도와 습도값을 전송하시오!(딥슬립일때 7.2ma/전송시 80~110)

![489-6_bb](https://user-images.githubusercontent.com/106683637/171844329-14e5d0f3-f000-4b40-b124-7627686d7424.jpg)
  
7.노드에 Co2센서(MH-Z19)를 연결해서 이산화탄소농도와 온도를 전송하시오!(Software Serial은 이유는 잘 모르겠지만 작동이 안되어서 Hardware Serial로 작동시킴/딥슬립일때 11.3ma/전송시 100~160ma) 주의 USB로 연결된 시리얼모니터에 결과 안나옴!

![489-7_bb](https://user-images.githubusercontent.com/106683637/171844325-59012749-8eea-45d7-b655-f917a67613bd.jpg)
  
관련라이브러리(LoRa/0.8.0)
https://github.com/sandeepmistry/arduino-LoRa
  
(Machine translation)

It's Nokanda's LoRa series that I've been working on for a while!
In this episode, we will check if the LoRa module sx1276 works normally on the Wemos d1 mini board that Nokanda recently purchased and apply deep sleep!

Two boards exchange messages with LoRa. The sensor board sends data to LoRa, and then deepsleeps to ensure battery safety!

Here, the board with the sensor will be called a 'node' and the collecting board will be called a 'gateway'.

In other words, the sensor value is uploaded by a board that is installed somewhere, but the battery is attached, so it is a concept to conserve electricity!

Also, let's test the following things that were not done in existing LoRa!<BR>
1.Check the function to change txpower and measure the current consumption!<BR>
2.Check the sleep function of the LoRa module itself and measure the current consumption!<BR>
3.Check the difference in current consumption during deep sleep and not!<BR>
4. Prepare some sensors and try to transmit the sensor values!<BR>
(temperature and humidity, carbon dioxide, fine dust, DS18B20, illuminance sensor, etc.)<BR>
(Nokkanda at will)

(actually done)

*To upload the program to the board to which Deep Sleep is applied, follow the steps below!<BR>
1.First pull out the line connected to RST and D0<BR>
2.If there is something connected to D3, unplug it first!<BR>
3.Upload the program!<BR>
4.Reconnect what you pulled out in (1) and (2)!<BR>

1. An example of connecting the sx1276 module to the Wemos d1 mini board to check whether two boards consisting of a gateway and a node can communicate in both directions!

2. (Code is the same as 1) Measure the amount of current consumed by the gateway and node in 1 with a multimeter and attach the result! (Usually 85, maximum 120 when sending a message)

3. Measure the amount of current consumed when the tx power sent from the gateway and node is increased to 20! (Check the increase from 120mA to 135mA)

4. Check how the sleep function works in the LoRa library!
  
5. Deepsleep the node with the sensor at the appropriate timing! (Example of the basic form of LoRa+wemos d1 mini+ deepsleep) (4.3ma in deep sleep/about 80~100ma when transmitting data)

6. Connect the temperature and humidity sensor (DHT-11) to the node and transmit the temperature and humidity values! (7.2mA in deep sleep/80~110 in transmission)

7. Connect the Co2 sensor (MH-Z19) to the node and transmit the carbon dioxide concentration and temperature! 160ma) Caution No results are displayed on the serial monitor connected via USB!

Related Libraries (LoRa/0.8.0)
https://github.com/sandeepmistry/arduino-LoRa
