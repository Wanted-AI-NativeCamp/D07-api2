# 독서 챌린지 (`features/reading`)

**담당:** 팀원 B · **PRD:** Epic C

오늘 읽을 책 추천 → 읽을 분량 체크 → 한 줄 감상 기록.

## 만들 것
- C-1 오늘의 책 추천 (P0): Open Library API, 관심 주제 기반, 읽은 책 제외, 쪽수 없으면 직접 입력
- C-2 읽을 분량 체크 (P0): 하루 목표, 진행률 바, 달성 스티커, 연속 달성 일수
- C-3 한 줄 감상 기록 (P0): 책별·날짜별 최대 100자, 수정·삭제

## 병합 규칙
- `__init__.py`는 `page()`, `ROUTE`, `get_today_summary()`만 내보낸다. `ROUTE = "reading"`. 홈 요약 카드에 오늘 읽은 분량을 보여줄 수 있게 한다.
- `st.set_page_config`는 `page()` 안에서 부르지 않는다. 단독 실행 파일 `dev.py`에서만 부른다.
- 위젯 `key`, `st.session_state` 키, 저장소 이름에 `reading_` 접두사를 붙인다.
- Open Library 호출 코드는 이 폴더의 `clients/`에 둔다. 책 검색 결과는 `st.cache_data(ttl=86400)`로 캐시한다.
- 저장 방식은 미정(PRD 13장)이므로 저장 코드는 `storage.py` 한 파일에 모은다.
- 다른 서비스와 직접 연결되는 부분은 없다. 단독으로 끝까지 동작해야 한다.
- 색·글꼴은 `.streamlit/config.toml` 테마와 `shared/` 스타일 헬퍼만 쓰고, 전역 CSS는 넣지 않는다.
- 이 폴더 밖의 파일은 수정하지 않는다.

## 단독 실행
```bash
streamlit run features/reading/dev.py   # 앱 골격이 올라온 뒤 사용
```
