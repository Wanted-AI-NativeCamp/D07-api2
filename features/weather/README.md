# 날씨 + 오늘 코디 (`features/weather`)

**담당:** 팀원 E · **PRD:** Epic F

오늘 날씨를 보여주고, 체감온도에 맞는 옷차림을 추천한다. 날씨 조회는 홈과 오늘의 한 끼도 가져다 쓴다.

## 만들 것
- F-1 오늘 날씨 (P0): 현재 기온·체감온도·강수·최고/최저·시간대별 예보, 캐시 10분
- F-2 오늘의 코디 추천 (P0): 체감온도 구간별 상의·하의·겉옷, 비·눈·강풍·자외선 준비물, 일교차 10℃ 이상이면 겉옷 문구, 일러스트

## 병합 규칙
- `__init__.py`는 `page()`, `ROUTE`, `get_today_summary()`에 더해 **`get_weather(lat, lng)`**를 내보낸다. `ROUTE = "weather"`
- `get_weather`의 반환 형태는 `{"temp", "feels_like", "precip", "min", "max", "hourly"}`이며, 홈과 오늘의 한 끼(팀원 A)가 병합 시 이 함수를 사용한다. 반환 형태를 바꿀 때는 먼저 팀원 A와 합의한다.
- 날씨 결과는 `st.cache_data(ttl=600)`로 캐시한다. 홈과 한 끼가 같은 날씨를 쓰므로 중복 호출이 생기지 않게 한다.
- `st.set_page_config`는 `page()` 안에서 부르지 않는다. 단독 실행 파일 `dev.py`에서만 부른다.
- 위젯 `key`, `st.session_state` 키에 `weather_` 접두사를 붙인다.
- 날씨 API 호출 코드는 이 폴더의 `clients/`에 두고, 키(`WEATHER_KEY`)는 `st.secrets`로만 읽는다. 날씨 API 선택(기상청 또는 OpenWeather)은 PRD 13장의 미정 항목이다.
- 현재 위치는 브라우저에서 바로 가져오기 어렵다. 수동 지역 선택을 기본으로 한다. (PRD FR-014)
- 색·글꼴은 `.streamlit/config.toml` 테마와 `shared/` 스타일 헬퍼만 쓰고, 전역 CSS는 넣지 않는다.
- 이 폴더 밖의 파일은 수정하지 않는다.

## 단독 실행
```bash
streamlit run features/weather/dev.py   # 앱 골격이 올라온 뒤 사용
```
