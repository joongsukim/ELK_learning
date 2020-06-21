# **Elastic Stack에 대한 사전 조사** 

## **Elastic Stack이란?**
사용자가 서버나 데이터베이스로부터 원하는 데이터를 실시간으로 수집하고 검색,분석하여 시각화 시키는 오픈소스 서비스이다. 기존의 ELK Solution(Elastic Search + Logstash+ Kibana)에 beats를 추가시켜서 Elastic Stack이라고 부른다.


## **Elastic Search**
아파치 루신을 기반으로 만든 분산 검색엔진으로 깃허브, 이베이, 가디언 같은 기업이 엘라스틱서치 기술로 내부 검색 기능을 구축했다.정형,비정형,위치정보,메트릭 등 원하는 방법으로 다양한 유형의 검색을 수행하고 결합할 수 있다. JSON 문서 형태로 데이터를 저장하며 각 문서는 일련의 키와 그에 해당되는 값을 서로 연결한다.

 **구조**
 1. Cluster
 가장 큰 시스템 단위로 1개 이상의 노드로 이루어진 노드의 집합
 각각의 클러스터는 데이터의 접근과 교환을 할 수 없는 독립적인 시스템

 2. Node
 Elastic Search를 구성하는 단위 프로세스
 역할에 따라 Master-eiligible, Data,Ingest,Tribe노드로 구분 가능

 3.Index /Shard/Replica
 index는 관계형 데이터베이스 관리 시스템의 index와 동일
 sharding은 데이터를 분산해서 저장하는 방법을 의미하며 한개의 인덱스를 다수의 shard로 나눔
 replica는 또 다른 형태의 shard로써 노드를 손실했을 경우 데이터의 신뢰성을 위해 샤드들을 복제 


## **Logstash**
엘라스틱 검색엔진에서 제공하는 데이터 수집 엔진이다. 기본적으로 beats와 같은 데이터 수집기에서 바로 log 저장소인 Elastic Search으로 바로 데이터를 전송할 수도 있지만 재처리 과정이 필요한 데이터의 경우 Logstash에서 재처리 과정을 거친 후 Elastic Search로 보낸다. 파이프라인으로 구성되는데 크게 보면 input에서 데이터를 받아들이면 filter에서 데이터를 가공한 후 output으로 데이터를 출력하는 방식이다. 각 단계는 개발자가 마음대로 조절해서 민감한 필드를 제외시키거나 익명화시키거나 정형화시키는 등 개발자가 원하는 데이터 형식으로 가공할 수 있다. 또한 input은 beats뿐만 아니라 nginx등 다른 곳에서도 데이터를 받을 수 있으며 output또한 Elastic Search말고도 다양한 출력을 지원한다.


## **Kibana** 
간단하게 말하면 Elastic Search에 저장되는 모든 데이터를 즉각적으로 시각화하는 도구이다. 
주요 기능:
1. Discover
Elastic Search에서 저장된 데이터를 한눈에 확인할 수 있는 메인페이지

2. Visualize
Elastic Search에서 수집된 결과를 시각화하여 표현 
Area chart,Data chart,Line chart등 다양한 종류의 차트를 지원

3. Dashboard 
Visualize를 통해 시각화된 객체를 모아 하나의 Dashboard에 배치하여 한눈에 볼 수 있게 해줌.

4. Setttings
데이터 시각화에 대한 모든 설정을 변경


## **Beats**
경량 에이전트로 설치되어서 각종 데이터를 Logstash 또는 Elastic Search로 전송하는 데이터 수집기이다. 모든 유형의 데이터를 수집하는 만큼 각 유형마다 수집기가 다르다 .
- Filebeat: 서버에서 로그와 피일을 경량화된 방식으로 전달해서 보다 작업을 보다 간편하게 만들어준다. Logstash가 과도한 데이터 처리로 인해 과부하가 걸릴 경우 Filebeat에서 자체적으로 로그를 수집하는 작업 속도를 늦춤으로써 flow control을 하는 특징이 있다.
- Packetbeat: 간단하게 말하자면 경량 네트워크 패킷 분석기이다. 네트워크 트래픽 검색 및 분석에 유용하게 쓰이며  디스크를 spooling을 위한 완충 기억 장치로 씀으로써 비교적 신뢰성 있는 데이터 전송을 보장한다.
- Winlogbeat:모든 윈도우 이벤트 로그 채널에서 데이터를 읽어내는 데이터 수집기이다. 
이외에도 데이터의 유형에 따라 Metircbeat,Auditbeat,Heartbeat등 다양한 데이터 수집기를 사용할 수 있다.





