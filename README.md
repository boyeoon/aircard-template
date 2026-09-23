# AirCard 스킨 프레스

Apple Wallet 카드 스킨을 [AirCard](https://github.com/Mak5er/AirCard)가 요구하는 규격에 정확히 맞춰 만드는 웹 도구입니다.

**→ https://boyeoon.github.io/aircard-template/**

빌드 도구도 서버도 없는 단일 HTML 파일이고, 이미지 처리는 전부 브라우저 안에서 끝납니다. 업로드하는 사진은 어디로도 전송되지 않습니다.

---

## 규격

| 항목 | 값 |
| --- | --- |
| 크기 | **1536 × 969 px** |
| 비율 | 1.5852 (ISO/IEC 7810 ID-1 신용카드 비율과 거의 동일) |
| 형식 | PNG · RGBA |
| 배치 | aspect-fill 센터 크롭 |

AirCard의 `prepareCardImage()`가 입력 이미지를 `CGSize(width: 1536, height: 969)`로 맞춘 뒤,
같은 PNG를 `cardBackgroundCombined@3x.png`와 `cardBackgroundCombined@2x.png`로 쓰고
`sips`로 `cardBackgroundCombined.pdf`까지 만들어 기기에 기록합니다.
그래서 정확한 규격의 원본 한 장이면 충분합니다.

> 출처: [`AirCardApp.swift`](https://github.com/Mak5er/AirCard/blob/main/AirCardApp.swift) → `prepareCardImage()`, [`card_assets.py`](https://github.com/Mak5er/AirCard/blob/main/card_assets.py)

---

## 기능

- **프리셋 4종** — 티타늄, 미드나이트 포일, 스이카, 파스모. 모두 캔버스에서 절차적으로 생성되므로 외부 이미지 요청이 없습니다.
  - 스이카·파스모는 실제 교통카드의 배색, 웨이브 형태, 워드마크 배치, IC 마크를 따라 그립니다. 마스코트 일러스트(스이카 펭귄, 파스모 로봇)는 별개 저작물이라 포함하지 않았습니다. 필요하면 사진 불러오기로 직접 넣을 수 있습니다.
- **사진 배치** — 드래그로 위치, 휠로 확대, 회전. AirCard와 동일한 cover 크롭 규칙을 그대로 재현해 잘려나갈 부분을 미리 확인합니다.
- **보정** — 밝기, 대비, 채도, 흐림
- **마감** — 비네팅, 그레인, 틴트
- **레터링** — 서체 4종, 9분할 위치, 크기, 자간, 색, 그림자
- **가이드** — 둥근 모서리 미리보기(1536 기준 약 85px)와 안전 영역 오버레이. 내보내는 PNG는 항상 모서리 없는 사각형이고, 둥근 모서리는 Wallet이 직접 마스킹합니다.

---

## 내보낸 다음

1. 아이폰을 USB로 연결하고 잠금 해제 · 신뢰 상태로 둡니다.
2. AirCard의 **Wallet Cards** 탭에서 **Scan Cards**를 누릅니다.
3. 아이폰에서 측면 버튼을 두 번 눌러 Apple Pay를 열고, Face ID 인증 후 카드를 탭해 인식시킵니다.
4. 카드 목업에 내보낸 PNG를 끌어다 놓고 **Flash Skins**를 누릅니다.
5. 아이폰에서 Wallet 앱을 완전히 종료하면 새 디자인이 보입니다.

---

## 로컬에서 보기

```sh
git clone https://github.com/boyeoon/aircard-template.git
cd aircard-template
open index.html
```

의존성이 없어 파일을 브라우저로 바로 열면 됩니다. 외부 요청은 Google Fonts 스타일시트 하나뿐입니다.

---

## 배포

`main` 브랜치 루트를 GitHub Pages가 그대로 서빙합니다. `index.html`을 수정하고 푸시하면 1~2분 안에 반영됩니다.

---

카드 스킨을 실제로 적용하려면 [AirCard](https://github.com/Mak5er/AirCard)(macOS)가 필요합니다. 이 저장소는 그 입력 이미지를 만드는 도구일 뿐, AirCard와는 별개 프로젝트입니다.
