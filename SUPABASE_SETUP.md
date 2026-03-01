# Supabase 설정 가이드

링크를 공유한 모든 사용자가 랭킹과 선물 코드를 공유하려면 Supabase 프로젝트를 설정해야 합니다.

## 1. Supabase 프로젝트 생성

1. [supabase.com](https://supabase.com) 접속 → **Start your project**
2. GitHub으로 로그인 후 **New Project** 생성
3. 프로젝트 이름, 비밀번호 설정 후 생성 (1~2분 소요)

## 2. 테이블 생성

좌측 **Table Editor** → **New table**

### ranks 테이블
- Name: `ranks`
- Columns:
  - `id` — bigint, Primary key, Identity (자동 증가)
  - `name` — text
  - `grade` — text
  - `score` — int4 (기본값 0)
  - `level` — int4 (기본값 1)
  - `date` — text
  - `created_at` — timestamptz (기본값: now())

### gift_codes 테이블
- Name: `gift_codes`
- Columns:
  - `id` — bigint, Primary key, Identity (자동 증가)
  - `name` — text
  - `grade` — text
  - `code` — text
  - `date` — text
  - `duration_seconds` — int4 (nullable)
  - `created_at` — timestamptz (기본값: now())

## 3. RLS(Row Level Security) 정책

각 테이블에서 **RLS** 탭 → **Enable RLS** 켜기

### ranks 정책
| Policy name      | Allowed operation | Target roles | Expression |
|------------------|-------------------|--------------|------------|
| allow_read_ranks | SELECT            | anon         | true       |
| allow_insert_ranks | INSERT          | anon         | true       |
| allow_delete_ranks | DELETE          | anon         | true       |

### gift_codes 정책
| Policy name          | Allowed operation | Target roles | Expression |
|----------------------|-------------------|--------------|------------|
| allow_read_gift_codes  | SELECT          | anon         | true       |
| allow_insert_gift_codes | INSERT        | anon         | true       |

## 4. API 키 설정

1. **Project Settings** → **API**
2. **Project URL**과 **anon public** key 복사
3. `index.html`과 `admin.html`에서 아래 부분 수정:

**index.html** (약 1195번 줄):
```javascript
var SUPABASE_URL = 'https://YOUR_PROJECT_ID.supabase.co';  // 본인 URL로 교체
var SUPABASE_ANON_KEY = 'eyJ...';  // 본인 anon key로 교체
```

**admin.html** (약 87번 줄):
```javascript
var SUPABASE_URL = 'https://YOUR_PROJECT_ID.supabase.co';  // index.html과 동일하게
var SUPABASE_ANON_KEY = 'eyJ...';  // index.html과 동일하게
```

⚠️ 두 파일에 **같은 값**을 넣어야 합니다.

## 5. 완료 후 확인

- 링크를 공유한 모든 사용자가 같은 랭킹을 보는지 확인
- 엔딩 후 선물 코드가 표시되는지 확인
- admin.html에서 랭킹과 선물 코드 수령 현황이 표시되는지 확인
