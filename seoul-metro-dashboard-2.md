
## 2. Kibana 대시보드


먼저 아래 명령으로 데이터 색인이 끝났는지 확인합니다. 전체 도큐먼트 수는  `"count" : 2007500` 입니다.

```
GET seoul-metro-logs-2018/_count
```

### Kibana 인덱스 패턴 생성

인덱스 패턴은 elasticsearch 인덱스를 식별하는데 사용되고 필드를 구성하는데 사용

- **Management > Kibana : Index Patterns** 메뉴로 이동
- **Create Index Pattern** 버튼 클릭
- **Index pattern** 입력폼에 `seoul-metro-logs*` 입력 후 **Next step** 클릭
- **Time Filter field name** 입력폼에 `@timestamp` 선택 후 **Create index pattern** 버튼 클릭

`seoul-metro-logs*` 인덱스 패턴이 생성 된 후 Discover 메뉴에서 데이터를 확인합니다.

- **Discover** 메뉴로 이동
- 저장된 인덱스 패턴 중 `seoul-metro-logs*` 를 선택
- 타임피커에서 날짜를 `2018-01-01` ~ `2019-01-01` 로 선택
- 데이터 확인

### 대시보드 저장

- **Dashboard** 메뉴로 이동
- **Create new dashboard** 버튼 클릭
- Add > 저장한 Visualization 선택
- Save : "서울 지하철 승하차인원" + 시간까지 같이 저장.

Visualization 추가 될 때 마다 위 과정 반복합니다.

### Visualizations

- **Visualizations** 메뉴로 이동
- **Create new visualization** 버튼 클릭

#### Metric : 승차인원 수, 하차인원 수, 전체인원 수

- **Metric** 선택
- **seoul-betro-logs\*** 인덱스 패턴 선택
- Metric 메뉴에서 전체 승차인원 추가
  - Aggregations : Sum
  - Field : `people.in`
  - Custom Labe : "전체 승차인원"
  - ▶️ 버튼 눌러 변경 사항 반영
- Metric 메뉴에서 전체 하차인원 추가
  - + Add 클릭해서 메트릭 추가
  - Aggregations : Sum
  - Field : `people.out`
  - Custom Labe : "전체 승차인원"
  - ▶️ 버튼 눌러 변경 사항 반영
- Metric 메뉴에서 전체 힘계 추가
  - Field : `people.total` 로 하고 다른 부분들은 반복
- options 탭으로 이동
  - style > Font Size : 20pt 정도로 조절

Save : "seoul-metro: 인원 수" 로 저장





