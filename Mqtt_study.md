# MQTT

## MQTT란?

- 경량의 publish/subscibe 메세징 프로토콜

- 메세지를 publish하고 구독자들은 관심있는 메세지를 구독하는 방식

- publisher와 subscriber들은 모두 broker의 client 

<img width="565" alt="스크린샷 2020-07-06 오전 11 43 58" src="https://user-images.githubusercontent.com/60679342/86550696-0cd08c80-bf7e-11ea-8fb4-30b955e144fc.png">

## 토픽 

- pub과 sub은 토픽을 기준으로 작동

- 슬래시를 이용해서 계층적으로 구성  (예: 하드디스크의 상태 측정 메세지를 위한 topic -> /sensors/node_name/temperature/harddisk)

-app들은 관심있는 topic을 구성하거나 발행

## MQTT broker 

- publisher와 subscriber들이 서로 메세지를 주고받을 수 있게 중계해주는 역할 

- 종류: Mosquitto , HiveMQ , mosca , ActiveMQ, RabbitMQ 

## MQTT QoS 


### QoS란?

- 서비스의 질을 보장해주는 레벨

- QoS를 지켜야할 정도를 등급으로 나누는데, MQTT에는 3가지 level로 정의

<img width="644" alt="스크린샷 2020-07-06 오전 11 34 06" src="https://user-images.githubusercontent.com/60679342/86550307-07bf0d80-bf7d-11ea-93bb-660672384795.png">


### QoS level0

- 보내고 메세지를 저장하지 않음 

- 전송이 성공하지 않으면 전송은 실패한 상태로 끝

### QoS level1

- 정상적으로 통신할경우 반드시 한번 이상은 전달

- ack message가 loss될 경우 , 중복 전송 발생 

### QoS level2

- 메세지는 한번 전달

- 메세지의 handshaking과정을 추척

- 신뢰성있는 전송을 보장하지만 성능 저하 

