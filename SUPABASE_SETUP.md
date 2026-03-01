# Supabase 설정 가이드

링크를 공유한 모든 사용자가 랭킹과 선물 코드를 공유하려면 Supabase 프로젝트를 설정해야 합니다.

⚠️ **Supabase**는 supabase.com에서 진행합니다. GitHub이 아닙니다.

---

## 1. Supabase 프로젝트 생성 (supabase.com)

1. 브라우저에서 **[supabase.com](https://supabase.com)** 접속
2. 우측 상단 **"Start your project"** 클릭
3. 로그인:
   - **GitHub** 또는 **Google** 계정으로 로그인
   - (또는 이메일/비밀번호로 가입)
4. 로그인 후 **Organization** 선택 또는 생성
   - 처음이면 "Create a new organization" → 이름 입력 후 생성
5. **"New project"** 버튼 클릭
   - Organization 선택
   - Project name: 예) `find-the-words`
   - Database Password: 설정 후 기억해 두기
   - Region: 가장 가까운 지역 선택
6. **"Create new project"** 클릭 → 생성 완료될 때까지 1~2분 대기

---

## 2. 테이블 생성

Supabase 대시보드에서:

1. 왼쪽 메뉴 **"Table Editor"** 클릭
2. **"New table"** 클릭

### ranks 테이블

- **Name**: `ranks`
- **Columns** 추가 (기본 `id` 제외):

| Column name | Type   | Default     | Nullable |
|-------------|--------|-------------|----------|
| name        | text   | -           | No       |
| grade       | text   | -           | Yes      |
| score       | int4   | 0           | No       |
| level       | int4   | 1           | Yes      |
| date        | text   | -           | Yes      |
| created_at  | timestamptz | now() | Yes   |

- **Save** 클릭

### gift_codes 테이블

1. 다시 **"New table"** 클릭
2. **Name**: `gift_codes`
3. **Columns** 추가:

| Column name     | Type      | Default | Nullable |
|-----------------|-----------|---------|----------|
| name            | text      | -       | No       |
| grade           | text      | -       | Yes      |
| code            | text      | -       | No       |
| date            | text      | -       | Yes      |
| duration_seconds| int4      | -       | Yes      |
| created_at      | timestamptz | now() | Yes   |

- **Save** 클릭

---

## 3. RLS(Row Level Security) 정책

각 테이블에서:

1. 해당 테이블 클릭 (ranks 또는 gift_codes)
2. 상단 **"RLS"** 탭 클릭
3. **"Enable RLS"** 스위치 켜기

### ranks 정책 (2개)

**정책 1: 읽기 허용**
- **"New Policy"** → **"For full customization"**
- Name: `allow_read_ranks`
- Allowed operation: **SELECT**
- Target roles: `anon`
- USING expression: `true`

**정책 2: 쓰기 허용**
- **"New Policy"** → **"For full customization"**
- Name: `allow_insert_ranks`
- Allowed operation: **INSERT**
- Target roles: `anon`
- WITH CHECK expression: `true`

### gift_codes 정책 (2개)

**정책 1: 읽기 허용**
- Name: `allow_read_gift_codes`
- Allowed operation: **SELECT**
- Target roles: `anon`
- USING expression: `true`

**정책 2: 쓰기 허용**
- Name: `allow_insert_gift_codes`
- Allowed operation: **INSERT**
- Target roles: `anon`
- WITH CHECK expression: `true`

> 랭킹 삭제 정책은 사용하지 않습니다. 초기화가 필요하면 Supabase 대시보드에서 테이블 데이터를 직접 삭제하세요.

---

## 4. API 키 확인

1. 왼쪽 하단 **"Project Settings"** (톱니바퀴 아이콘) 클릭
2. **"API"** 메뉴 선택
3. **Project URL**과 **Project API keys**의 **anon public** 복사

---

## 5. 코드에 API 키 입력

`index.html`과 `admin.html` 상단에 이미 Supabase 설정이 있으면, Project URL과 anon key만 확인하면 됩니다.

---

## 6. 완료 후 확인

- 게임 페이지에서 점수 저장 → 랭킹 화면에 반영되는지 확인
- 다른 기기/브라우저에서도 같은 랭킹이 보이는지 확인
- 엔딩 후 선물 코드가 표시되는지 확인
- admin.html에서 랭킹·선물 코드 현황이 표시되는지 확인
