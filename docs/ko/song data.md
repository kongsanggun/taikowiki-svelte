# 곡 데이터

## 타입스크립트 타입

`SongData` 타입은 `src/lib/module/song/types.ts` 파일에 있습니다.

## 규칙칙

### 제목

- `제목` 은 곡의 일본어 원제를 의미합니다.
- 만약 곡이 **아케이드 버전**에 수록되어있고, **동더히로바**에서 찾을 수 있다면, 곡 제목은 **동더히로바**에 쓰인 것과 완전히 동일하게 사용합니다.

### 곡 번호

- `곡 번호`는 곡을 특정하기 위해 사용합니다.
- 만약 곡이 **아케이드 버전**에 수록되어있고, **동더히로바**에서 찾을 수 있다면, 곡 번호는 **동더히로바**에 쓰인 것과 완전히 동일하게 사용합니다.
- 만약 곡이 **아케이드 버전**에 수록되어있지 않다면, 임의의 문자열을 사용합니다.

### 한국어 / 영어 제목

- 한국어 / 영어 제목은 **아케이드 버전**을 기준으로 합니다.
- 만약 곡이 **아케이드 버전**에 수록되어있지 않다면, **가장 최신의 콘솔 버전**을 기준으로 합니다.

### 한국어 / 영어 별칭 (비공식 번역)

- 곡의 공식 번역이 불만족스러운 경우가 있기 때문에, 별칭 (비공식 번역)을 사용할 수 있습니다.
- 예시
    | 제목 | 공식 한국어 번역 | 비공식 한국어 번역 |
    | :-: | :-: | :-: |
    | 六兆年と一夜物語 | 로쿠쵸넨토이치야모노가타리 | 육조년과 하룻밤 이야기 |
    | 魑魅魍魎 | Chimi Moryo | 이매망량 |

### 로마자
- `로마자`는 일본어 원제의 발음을 로마자로 쓴 것입니다. 
- 만약 일본어 원제가 영어를 가나로 표기한 것이라면, 일본어 발음을 로마자로 표기한 것이 아닌 영어를 사용합니다.
- 예시
    | 제목 | 로마자 |
    | :-: | :-: |
    | 束ね糸 | Tabaneito |
    | シカ色デイズ | Shikairo Days |