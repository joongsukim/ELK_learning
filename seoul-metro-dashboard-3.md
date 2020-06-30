## google analytics사용하기

## timestamp 필드에서  기록시간 추출하기 

<img width="642" alt="script를 이용해서 timestamp에서 hour of day 추출 " src="https://user-images.githubusercontent.com/60679342/86073121-1d848c80-babe-11ea-8dfd-10c10bbc4889.png">

- dev tool에서 위와 같은 쿼리를 이용해서 hour of day라는 필드를 생성

- script field를 사용

  - 하루 24시간중에 해당 시간대만 추출하는 script
  
  - "lang": "PAINLESS"는 default이므로 안써도 가능
  
  - "source" 필드에 함수를 생성(timestamp의 value값을 추출해서 getHourOfDay()함수를 통해서 시간대 추출 )


<img width="485" alt="hour of day 필드 생성" src="https://user-images.githubusercontent.com/60679342/86073090-0e054380-babe-11ea-8068-1360e449977d.png">

- 결과값을 보면 시간대가 추출된 것을 확인 









### google analytics란?

- 웹사이트 방문자의 데이터를 수집해서 분석함으로써 온라인 비즈니스의 성과를 측정하고 개선하는 데 사용하는 웹로그분석 도구

