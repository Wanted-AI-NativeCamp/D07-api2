# 밥때 손님 (`features/guest`)

**담당:** 팀원 C · **PRD:** Epic D (서비스 이름은 가제)

끼니를 기록하면 강아지·고양이 손님이 찾아오고, 만난 손님이 도감 카드로 쌓인다.

## 만들 것
- D-1 손님 방문 (P0): 끼니 기록 시 1마리, 품종은 가중 랜덤, 하루 최대 3회, 수정해도 중복 방문 없음, 희귀도 확률은 설정 파일
- D-2 도감 (P0): 품종 카드 격자, 미발견은 실루엣, 수집률, 개/고양이 필터, 카드 상세
- D-3 연속 일수 (P1), D-4 단골 레벨 (P1)

## 병합 규칙
- `__init__.py`는 `page()`, `ROUTE`, `get_today_summary()`만 내보낸다. `ROUTE = "guest"`
- `st.set_page_config`는 `page()` 안에서 부르지 않는다. 단독 실행 파일 `dev.py`에서만 부른다.
- 위젯 `key`, `st.session_state` 키, 저장소 이름에 `guest_` 접두사를 붙인다.
- 개발 중에는 "끼니 기록됨" 이벤트를 발생시키는 테스트 버튼으로 단독 검증한다. 병합 시 `meal_logged { meal_log_id, slot, date }` 수신으로 교체한다. (발행은 팀원 A, 전달 방식은 PRD 13장 미정)
- 다른 서비스와의 참조는 `GuestVisit.meal_log_id` 하나뿐이다. 병합 전에는 목 ID를 쓴다.
- 확률표와 품종 목록은 설정 파일(`toml`/`json`)로 분리한다.
- 저장 방식은 미정(PRD 13장)이므로 저장 코드는 `storage.py` 한 파일에 모은다.
- 일러스트는 직접 제작하거나 라이선스를 확인한 것만 쓴다. MVP는 품종 20종으로 시작한다.
- 색·글꼴은 `.streamlit/config.toml` 테마와 `shared/` 스타일 헬퍼만 쓰고, 전역 CSS는 넣지 않는다.
- 이 폴더 밖의 파일은 수정하지 않는다.

## 단독 실행
```bash
streamlit run features/guest/dev.py   # 앱 골격이 올라온 뒤 사용
```
