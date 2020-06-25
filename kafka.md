# kafka에 대한 간단한 이해 

## kafka란?

   - 
   
   
   
   
   ## 토픽 
   
   - db나 파일시스템의 폴더와 유사한 성질 가짐
   
   - 토픽에 데이터를 전송하는 producer와 데이터를 받는 consumer
   
   - 토픽 안에는 1개 이상의 partition으로 구성 
   
   - partition는 하나의 큐라고 볼 수 있는데 해당 데이터를 consumer가 가져가더라도 사라지지 않는 특성있음
   
   - 위와 같은 특성으로 다양한 consumer들이 동일 데이터를 저장할 수 있음
   
   - partition 안에 저장된 데이터는 사전에 정의된 시간이나 용량을 넘어서면 삭제
   
   ## kafka producer
   
   ### kafka producer의 역할
   
   - Topic에 해당하는 메세지를 생성
   
   - 특정 Topic으로 데이터를 전송
   
   - 전송 실패할 경우 재전송 가능
   
   
