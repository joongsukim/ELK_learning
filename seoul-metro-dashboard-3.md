

## timestamp 필드에서  기록시간 추출하기 

<img width="642" alt="script를 이용해서 timestamp에서 hour of day 추출 " src="https://user-images.githubusercontent.com/60679342/86073121-1d848c80-babe-11ea-8dfd-10c10bbc4889.png">

- dev tool에서 위와 같은 쿼리를 이용해서 hour of day라는 필드를 생성

- script field를 사용

  - 하루 24시간중에 해당 시간대만 추출하는 script
  
  - "lang": "PAINLESS"는 default이므로 안써도 가능
  
  - "source" 필드에 함수를 생성(timestamp의 value값을 추출해서 getHourOfDay()함수를 통해서 시간대 추출 )


<img width="485" alt="hour of day 필드 생성" src="https://user-images.githubusercontent.com/60679342/86073090-0e054380-babe-11ea-8068-1360e449977d.png">

- 결과값을 보면 시간대가 추출된 것을 확인 

- def 부분만 가져와서 index pattern에 script fields에 추가

<img width="641" alt="요일 만드는 해당 쿼리" src="https://user-images.githubusercontent.com/60679342/86074719-7144a500-bac1-11ea-9516-d172265f1f61.png">


- 위와같은 방법으로 요일도 분리

- 만든 script필드로 heat map 생성 

<img width="998" alt="heat map " src="https://user-images.githubusercontent.com/60679342/86075744-ab16ab00-bac3-11ea-9e76-86b7c33c238b.png">


- x축 ,y축을 나누어서 x축은 시간대별 y축은 요일로 구분 


## 파이프라인 생성

- logstash 와 같은 기능

- 파이프라인을 통해 특정 필드로부터 새로운 필드 추출 

<img width="658" alt="파이프라인 쿼리" src="https://user-images.githubusercontent.com/60679342/86076507-262c9100-bac5-11ea-9a6a-8b314ed15ee6.png">

- ctx를 사용하고 @datastamp같은 경우에는 특수문자가 포함되어 있어서 ['timestamp']형식

- 해당 파이프라인을 만든뒤 reindex로 해당 필드를 추가시킨 인덱스를 생성 

- reindex문 안에 pipeline을 추가 


### google analytics란?

- 웹사이트 방문자의 데이터를 수집해서 분석함으로써 온라인 비즈니스의 성과를 측정하고 개선하는 데 사용하는 웹로그분석 도구

