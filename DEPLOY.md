# GitHub Pages 배포 시 필요한 폴더

이 게임이 **음악과 그림**을 쓰려면 아래 폴더를 저장소에 **반드시** 넣어야 합니다.

## 폴더 구조 (프로젝트 루트 기준)

```
Cheerup-JohnRoss/
├── index.html          ← 메인 파일
├── assets/
│   ├── images/         ← 그림 파일
│   │   ├── intro.png
│   │   ├── john ross sad.png
│   │   ├── john ross happy.png
│   │   ├── ending.jpg
│   │   ├── castle_beige.png
│   │   ├── villain.png
│   │   └── buttonLong_beige.png
│   ├── sounds/         ← BGM·효과음
│   │   ├── Villatic_Animation.mp3
│   │   ├── The_Amazing_Digital_Circus.mp3
│   │   ├── punch.ogg
│   │   ├── crack.ogg
│   │   ├── place.ogg
│   │   ├── clear.ogg
│   │   ├── wolf.wav
│   │   ├── click.ogg
│   │   ├── wrong.ogg
│   │   ├── correct.ogg
│   │   └── National_Anthem_Instrumental_One_Verse.mp3   ← 엔딩 BGM (MP3 권장)
│   └── audio/
└── DEPLOY.md           ← 이 파일
```

## 올리는 방법

1. **드래그로 올릴 때**  
   `index.html`만 넣지 말고, **assets 폴더 전체**를 그대로 끌어다 놓기.

2. **Git으로 올릴 때**  
   `assets` 폴더가 프로젝트 안에 있는지 확인한 뒤:
   ```bash
   git add index.html assets
   git commit -m "Add assets for images and sounds"
   git push
   ```

## 확인

배포 후 브라우저에서 아래 주소가 404가 아니어야 합니다.

- https://bible-pipe.github.io/Cheerup-JohnRoss/assets/images/intro.png
- https://bible-pipe.github.io/Cheerup-JohnRoss/assets/sounds/Villatic_Animation.mp3
- https://bible-pipe.github.io/Cheerup-JohnRoss/assets/sounds/National_Anthem_Instrumental_One_Verse.mp3

위 주소가 열리면 그림·음악이 정상 로드됩니다.

**엔딩 BGM:** iOS·Safari는 OGG를 잘 재생하지 않습니다. OGG만 있다면 [CloudConvert](https://cloudconvert.com/ogg-to-mp3) 등으로 MP3로 변환한 뒤 `assets/sounds/National_Anthem_Instrumental_One_Verse.mp3` 로 넣으세요.
