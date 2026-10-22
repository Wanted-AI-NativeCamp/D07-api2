# 오늘의 한 끼 (`features/meal`)

**담당:** 팀원 A (홈과 겸임) · **PRD:** Epic B

날씨·시간대·주변 식당을 조합해 "지금 먹을 만한 메뉴"를 추천하고, 끼니를 기록한다.

## 만들 것
- B-1 상황 기반 메뉴 추천 (P0): 끼니 판별, 메뉴 3개 추천, 이유 문구, 다시 추천
- B-2 주변 식당 연결 (P0): 카카오 로컬 API, 반경 1km → 0건이면 3km 제안
- B-3 끼니 기록 (P0): 아침/점심/저녁 하루 1회, 수정·삭제

## 병합 규칙
- `__init__.py`는 `page()`, `ROUTE`, `get_today_summary()`만 내보낸다. `ROUTE = "meal"`
- `st.set_page_config`는 `page()` 안에서 부르지 않는다. 단독 실행 파일 `dev.py`에서만 부른다.
- 위젯 `key`, `st.session_state` 키, 저장소 이름에 `meal_` 접두사를 붙인다.
- 카카오 로컬 호출 코드는 이 폴더의 `clients/`에 두고, 키(`KAKAO_REST_KEY`)는 `st.secrets`로만 읽는다.
- 개발 중 날씨는 목 데이터를 쓰고, 병합 시 `get_weather(lat, lng)`(팀원 E)로 교체한다.
- 끼니를 기록하면 `meal_logged { meal_log_id, slot, date }` 이벤트를 발행한다. (팀원 C의 손님이 병합 시 수신. 전달 방식은 PRD 13장 미정)
- 저장 방식은 미정(PRD 13장)이므로 저장 코드는 `storage.py` 한 파일에 모은다.
- 색·글꼴은 `.streamlit/config.toml` 테마와 `shared/` 스타일 헬퍼만 쓰고, 전역 CSS는 넣지 않는다.
- 이 폴더 밖의 파일은 수정하지 않는다.

## 단독 실행
```bash
streamlit run features/meal/dev.py   # 앱 골격이 올라온 뒤 사용
```
