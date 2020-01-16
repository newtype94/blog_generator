---
title: 포트폴리오 - typesound
date: 2020-01-13 13:30:31
tags:
  - react.js
  - typescript
category:
  - 포트폴리오
  - 개인프로젝트
---

# 빠른 소개

피아노 웹이다.
많은 악기를 지원해서 어떤 곳에는 신디사이저 웹이라고 소개하기도 했다.
<img src="/image/typesound/main.JPG" width="60%" title="30px" alt="홈"></img>

## 운영 플랫폼(서비스 종료)

PC, Mobile 반응형 : www.typesound.net

## 사용 기술

|        | 사용 기술                 |
| ------ | ------------------------- |
| 호스팅 | iwinv(국산 클라우드 업체) |
| OS     | Ubuntu,                   |
| Client | ReactJS(Typescript)       |

## 기간

- 운영기간
  2019.09.04 ~ 2020.01.13
- 제작기간
  2019.08 ~ 2019.09

아래 사진들은 iwinv에서 실제 서버를 임대하고 도메인을 구입해 연동한 기록이다.
<img src="/image/typesound/domain.jpg" width="60%" title="30px" alt="도메인"></img>
<img src="/image/typesound/cloud.jpg" width="60%" title="30px" alt="클라우드"></img>

# 소개

## 차별점

1. 오른손(하늘색) 연주, 왼손(갈색) 연주를 양손으로 따로 입력할 수 있음

<img src="/image/typesound/guide.jpg" width="90%" title="30px" alt="가이드"></img>

2. 왼손 반주 패턴을 3가지 지원함

   <img src="/image/typesound/playing_-.JPG" width="40%" title="30px" alt="playing_-"></img>
   <img src="/image/typesound/playing_^.JPG" width="40%" title="30px" alt="playing_^"></img>
   <img src="/image/typesound/playing_v.JPG" width="40%" title="30px" alt="playing_v"></img>

3. 왼손 연주시 chord 마다 해당하는 소리를 mapping 해놓음

   <img src="/image/typesound/sound_-.JPG" width="60%" title="30px" alt="sound_-"></img>
   <img src="/image/typesound/sound_^.JPG" width="60%" title="30px" alt="sound_^"></img>

`/src/lib/chordNotes.ts`

```typescript
const chordNotes: { [x: string]: TSchordEnum[][] } = {
  // C
  [TSchordVariationEnum.CMajor]: [
    [TSchordEnum.C, TSchordEnum.E, TSchordEnum.G],
    [],
    []
  ],
  [TSchordVariationEnum.Cm]: [
    [TSchordEnum.C, TSchordEnum.Eb, TSchordEnum.G],
    [],
    []
  ],
  [TSchordVariationEnum.Cm6]: [
    [TSchordEnum.C, TSchordEnum.Eb, TSchordEnum.G, TSchordEnum.A],
    [],
    []
  ],
  // ....
  // ( CDEFGAB ) x (major,m,m6,m7,aug,dim,2,6,7,sus2,sus4) => 77개 패턴
  // ....
  [TSchordVariationEnum.B7]: [
    [TSchordEnum.B],
    [TSchordEnum.Eb, TSchordEnum.Gb, TSchordEnum.A],
    []
  ],
  [TSchordVariationEnum.Bsus2]: [
    [TSchordEnum.B],
    [TSchordEnum.Db, TSchordEnum.Gb],
    []
  ],
  [TSchordVariationEnum.Bsus4]: [
    [TSchordEnum.B],
    [TSchordEnum.E, TSchordEnum.Gb],
    []
  ]
};
```

# 개발 과정

## 음원 구하기

개발을 시작하기 전 우선 순위는 모든 옥타브를 아우르는 피아노 음원을 구하는 일이었다.
몇 일에 걸쳐 찾던 중, 우연히 fit이 맞는 github repository를 발견했다.
https://github.com/gleitz/midi-js-soundfonts
midi의 음원을 pre-rendering하였고, MIT 저작권으로 제공한다.
그리고 가장 큰 장점은 매우 많은 악기를 전 옥타브에 걸쳐 모아놓은 점이다.
(Thanks to gleitz!)

## reactJS의 사용 이유

기존의 피아노 웹들을 보면 대부분 flash를 사용하였고, 그나마 최신 웹이 jquery를 사용했다.
reactJS의 "상태 관리"라는 메인 컨셉을 활용하여 개발하면 차별성이 있을 것이라고 생각했다.
"키가 눌림"을 custom hook으로 정의하여, 문서객체마다 jquery onclick 이벤트를 연결할 일을 피했다.

`/src/hooks/useKeyPress.ts`

```typescript
function useKeyPress(targetKey: string) {
  const [keyPressed, setKeyPressed] = useState(false);

  function downHandler(event: KeyboardEvent) {
    if (event.key === targetKey) {
      setKeyPressed(true);
    }
  }

  const upHandler = (event: KeyboardEvent) => {
    if (event.key === targetKey) {
      setKeyPressed(false);
    }
  };

  useEffect(() => {
    window.addEventListener("keydown", downHandler);
    window.addEventListener("keyup", upHandler);
    return () => {
      window.removeEventListener("keydown", downHandler);
      window.removeEventListener("keyup", upHandler);
    };
  }, []);

  return keyPressed;
}
```

## typescript의 사용 이유

typescript는 type이나 enum을 미리 정의하여 javascript를 더 strict하게 쓸 수 있고
parameter의 interface를 정의하여 메서드 호출 시점에 내 입맛대로 정의한 parameter를 시각적으로 알 수 있다.
이 2가지를 해두면 개발 과정에 있어 타이핑시 자동예측을 해주어 개발속도가 빨라지며, 협업을 할 경우에도 더 유리해진다.
