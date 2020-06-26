# kafka에 대한 간단한 이해 

## kafka란?

   - 아파치 소프트웨어 재단이 스칼라로 개발한 오픈소스 메시지 브로커 프로젝트
   
   - 실시간 데이터 피드의 관리와 낮은 지연율과 높은 전송폭을 지원 
   
   - 다양한 곳에서 들어온 각각의 다른 데이터를 한 곳에서 실시간으로 관리 가능 
   
   ### 카프카를 안 사용할 경우
   
   <img width="671" alt="스크린샷 2020-06-25 오후 5 48 08" src="https://user-images.githubusercontent.com/60679342/85687847-32eb6680-b70c-11ea-9bdb-cf13c8e003f5.png">
   
   ### 카프카를 사용할 경우
   <img width="528" alt="스크린샷 2020-06-25 오후 5 47 26" src="https://user-images.githubusercontent.com/60679342/85688150-747c1180-b70c-11ea-843b-c6b650028929.png">
   
   다양한 곳에서 흘러들어온 데이터를 한 곳에서 관리할 수 있고 해당 데이터를 다른 프로그램들이 여러 곳에서 다운 받을 필요없이 kafka라는 거대한 큐에서 받을 수 있음
   
   
   
   ## 토픽 
   
   - db나 파일시스템의 폴더와 유사한 성질 가짐
   
   - 토픽에 데이터를 전송하는 producer와 데이터를 받는 consumer
   
   - 토픽 안에는 1개 이상의 partition으로 구성 
   
   - partition는 하나의 큐라고 볼 수 있는데 해당 데이터를 consumer가 가져가더라도 사라지지 않는 특성있음
   
   - 위와 같은 특성으로 다양한 consumer들이 동일 데이터를 저장할 수 있음
   
   - partition 안에 저장된 데이터는 사전에 정의된 시간이나 용량을 넘어서면 삭제
   
   ## Broker 
   
   
   ## kafka producer
   
   ### kafka producer의 역할
   
   - Topic에 해당하는 메세지를 생성
   
   - 특정 Topic으로 데이터를 전송
   
   - 전송 실패할 경우 재전송 가능
   
   
   ## kafka consumer
   
   ### kafka comsumer의 역할
    
    - topic의 partition으로부터 데이터 polling(데이터를 가져오는 것)
    
    - Partition offset 위치 기록 
      offset: partition에 있는 데이터 번호 
    
    - consuemr가 오류로 polling을 중지하더라도 추후에 offset을 이용하여 복구가능 
    
   ## Lag
   
   - 모니터링 지표중 하나
    
   - producer의 offset - comsumer의 offset의 차이를 기반으로 함
   
   - partition들 각각 lag값이 있으며 해당 토픽의 lag값들 중에서 가장 높은 값을 record-lag-max를 부름
   
   - Kafka consumer객체를 이용하여 현재 lag정보를 얻을 수 있는데 , record-lag-max값만 가져올 수 있으므로 해당 토픽의 다른 partition의 정상 작동은 파악하기 어려움 
   
   - Burrow를 사용하면 모든 lag값들의 정보를 파악 가능 
    
    
   ## Burrow
   
   - Apache 에서 내놓은 consumer log를 효과적으로 모니터링하기 위해 내놓은 오픈소스
   
   - go 언어로 제작
   
   ### Burrow의 특징
   
   - Multi Kafka cluster 지원: Kafka Cluster안에 있는 수 많은 partition들의 Lag정보를 burrow application 하나로 모니터링 가능 
   
   - Sliding window(센네에서 배운거 같이 어떤 일정한 범위를 유지하면서 이동)를 활용한 consumer의 status 확인: burrow는 수많은 consumer들의 상태를 error warning ok의 상태로 표현가능하게    만듬
   
     - warning상태 : producer의 데이터 전송 속도가 consumer의 데이터를 받는 속도보다 빨라서 lag값이 증가하는 경우
     
     - error상태: producer의 데이터를 전송하여서 producer의 offset값은 증가하는데 consumer은 데이터를 받지 않을 경우
     
     - ok상태 : 양쪽 모두 원할한 상태
   
   - http api 지원: 가장 널리 사용하는 http api를 제공함으로써 다양한 추가 생태계 구현 가능 
   
   
   
   
    
