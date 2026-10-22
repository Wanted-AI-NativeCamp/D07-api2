# 날씨 + 오늘 코디 (`features/weather`)

**담당:** 팀원 E · **PRD:** Epic F

오늘 날씨를 보여주고, 체감온도에 맞는 옷차림을 추천한다. 날씨 조회는 홈과 오늘의 한 끼도 가져다 쓴다.

## 만들 것
- F-1 오늘 날씨 (P0): 현재 기온·체감온도·강수·최고/최저·시간대별 예보, 캐시 10분
- F-2 오늘의 코디 추천 (P0): 체감온도 구간별 상의·하의·겉옷, 비·눈·강풍·자외선 준비물, 일교차 10℃ 이상이면 겉옷 문구, 일러스트

## 병합 규칙
- `index.ts`는 `Page`, `routes`, `getTodaySummary()`에 더해 **`getWeather(lat, lng)`**를 내보낸다. 반환 형태는 `{ temp, feelsLike, precip, min, max, hourly[] }`이며, 홈(팀원 A)과 오늘의 한 끼(팀원 A)가 병합 시 이 함수를 사용한다. 반환 형태를 바꿀 때는 먼저 팀원 A와 합의한다.
- 경로 `/weather`, 저장소·로컬 키 접두사 `weather_`, 서버 코드는 `api/weather/`, API 키 이름은 `WEATHER_KEY`
- 날씨 API 선택(기상청 또는 OpenWeather)은 PRD 13장의 미정 항목이다.
- 색·글꼴은 `shared/`의 디자인 토큰만 쓰고, 전역 CSS는 쓰지 않는다.
- 이 폴더 밖의 파일은 수정하지 않는다.
