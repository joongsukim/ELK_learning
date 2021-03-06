# 공공데이터를 이용한 서울시 지하철 대시보드

## 1. 공공데이터로부터 추출 ,색인, 매핑 및 탬플릿 설정 부분까지

### 프로그램 준비

- http://github.com/eskrug/elastic-demos를 clone

- elastic-demos/seoul-metro-logs 폴더로 이동

- data 디렉토리 생성 

### 공공 데이터 수집

서울 열린 데이터 광장 접속 : https://data.seoul.go.kr/

#### 지하철역 위치 정보

검색어: ** 서울시 역코드로 지하철역 위치 조회 **
 - json 파일로 다운로드
 - elastic-demos/seoul-metro-logs/source 파일에 저장
 
#### 다국어 역명 정보 

검색어 : ** 서울교통공사 연도별 일별 시간대별 역별 승하차 인원 **

- xslx 파일밖에 없으니 json 파일로 변환후 source 파일에 저장

- 변환할때 필드값들이 한글로 되어있으므로 전부 다 영어로 바꿔줘야함

### 역별 승하차 인원 데이터셋 

- 최근 파일 다운로드

- Excel 로 직접 편집 -> 1행 삭제 , B열 삭제

- 날짜 형식 변환  예) 2018-01-02 

- source 파일에 저장 

### 1호선~5호선 , 6호선 ~9호선 역별 전화번호부 저장 

- json파일로 다운 후 source directory 에 저장 


### 파일 변환 프로그램 실행

`elastic-demos/seoul-metro-logs` 경로 에서 npm 패키지를 설치합니다.
```
npm install
```

변환 프로그램을 실행합니다.
```
node bin/run.js
```
### 변환 프로그램을 한후

logstash 사용 


input {
  file {
    path => "/Users/joongsu/desktop/elastic/elastic-demos/seoul-metro-logs/data/seoul-metro-2018.logs"
    codec => "json"
    start_position => "beginning"
    sincedb_path => "/dev/null" 
  }
}

filter {
  mutate {
    remove_field => ["host","path","@version"]
  }
}

output {


 elasticsearch {
    hosts => "localhost"
    index => "seoul-metro-logs-2018"
 }
}


