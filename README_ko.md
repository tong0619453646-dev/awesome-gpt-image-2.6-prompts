<div align="center">

<a href="https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-gpt-image-2.6-prompts"><img src="assets/banner.jpg" alt="Awesome GPT Image 2.6 프롬프트" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-319_cases-111111)](README_ko.md#menu)
[![Try GPT Image 2.6 on APIKO](https://img.shields.io/badge/Try_GPT_Image_2.6-on_APIKO-4F46E5)](https://apiko.app/ko/models/gpt-image-2.6-flare?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=model_try)
[![GPT Image 2.6 API docs](https://img.shields.io/badge/GPT_Image_2.6-API_docs-111111)](https://apiko.app/docs/api-manual/image-series/gpt-image-2.6-flare/images?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Default-4F46E5)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-Current-111111)](README_ko.md)

</div>

# Awesome GPT Image 2.6 프롬프트

<a id="introduction"></a>
## 🌟 소개

**GPT Image 2.6 프롬프트 319개: 루프 GIF, 스티커 세트, 마크업 편집, 포스터, 제품 사진까지 결과와 함께 바로 복사해 쓸 수 있는 예시.**

GPT Image 2.6 프롬프트마다 실제로 나온 이미지나 GIF를 붙였습니다. 그대로 복사하거나 플레이그라운드로 보내 세부만 바꿔 보세요. GIF 결과물은 GitHub에서 바로 반복 재생됩니다.

검색과 필터는 [apiko.app/gpt-image-2-6-prompts](https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=intro).

> [!NOTE]
> 프롬프트는 작성자가 올린 원문 그대로라 대부분 영어입니다. 제목과 설명은 저희가 썼습니다. 모든 예시에 작성자와 원본 게시물 링크를 달았습니다.

<a id="quick-start"></a>
## 🚀 빠른 시작

**브라우저에서:** 모든 예시에 **APIKO에서 실행** 링크가 있습니다. [apiko.app](https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=browser)에서 해당 예시가 열리며, **사용**을 누르면 프롬프트가 GPT Image 2.6 플레이그라운드에 채워집니다.

**API로:** [APIKO API 키](https://apiko.app/ko/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=api_key)를 만든 뒤 비동기 작업을 생성하고, 이미지가 완성될 때까지 상태를 조회합니다.

```bash
export APIKO_API_KEY="your_key_here"

TASK_ID=$(curl -s https://api.apiko.app/v1/images/generations \
  -H "Authorization: Bearer $APIKO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "model": "gpt-image-2.6-flare",
  "prompt": "A minimalist poster of a paper boat on a calm lake at sunrise, the title \"Morning\" in bold serif type.",
  "size": "16:9",
  "resolution": "1k",
  "quality": "medium",
  "async": true
}' | python3 -c 'import json,sys; print(json.load(sys.stdin)["id"])')

# When status is "completed", the image is at data[0].url (kept for 24 hours).
while :; do
  TASK=$(curl -s https://api.apiko.app/v1/tasks/$TASK_ID \
    -H "Authorization: Bearer $APIKO_API_KEY")
  printf '%s\n' "$TASK"
  printf '%s' "$TASK" | grep -qE '"status": *"(completed|failed)"|"error": *\{' && break
  sleep 5
done
```

엔드포인트: `POST https://api.apiko.app/v1/images/generations` (작업 생성) · `GET https://api.apiko.app/v1/tasks/{id}` (상태와 결과 조회)

<a id="how-to-write"></a>
## ✍️ GPT Image 2.6 프롬프트 작성법

이 페이지의 프롬프트에 반복해서 나오는 네 가지 구조입니다.

- **루프 GIF** · `주체 + 동작 하나 + 시작 자세로 복귀 + 고정 카메라` — GIF 프롬프트는 동작 하나를 순서대로 적고, 시작 자세로 끝나게 해 루프를 잇고, 카메라가 움직이지 않는다고 밝힙니다. 프레임 수를 적는 경우도 많습니다.
- **마크업 편집** · `원으로 표시한 부분 + 바꿀 내용 + 나머지 유지` — 바꿀 곳에 원을 그리고 원마다 짧은 지시를 하나씩 적습니다. API는 같은 크기의 투명 오버레이로 이 표시를 받습니다.
- **같은 캐릭터로 여러 장** · `고정할 특징 + 장마다 동작이나 장면만 변경` — 스티커와 그림책 프롬프트는 유지할 머리 모양, 옷, 색을 먼저 적고 동작, 문구, 배경만 바꿉니다.
- **촬영 지시서** · `주체 + 빛 + 렌즈나 필름 + 질감` — 인물과 제품 프롬프트는 빛(창문 빛, 골든아워 역광), 렌즈나 필름 느낌, 보고 싶은 재질 디테일을 적습니다.

**예시에서 보이는 것**

- **GIF는 짧은 프롬프트로도 됩니다.** 여기 있는 루프 몇 개는 '자전거 타는 펠리컨'처럼 한 줄에서 나왔습니다. 긴 프롬프트는 동작 순서와 움직이지 않을 부분을 더합니다.
- **스티커 문구는 프롬프트에 직접.** 스티커 프롬프트는 문구를 따옴표로 묶고 위치를 정해, 여러 감정 스티커가 한 캐릭터를 공유하게 합니다.
- **재사용할 프롬프트엔 빈칸을.** 템플릿 프롬프트는 [object], [Brand Name]처럼 채울 부분을 대괄호로 표시하고 나머지는 고정합니다.
- **업로드한 이미지에 번호를.** 편집 프롬프트는 '두 번째 이미지의 개', '이미지 1'처럼 적어 어느 사진이 무엇을 제공하는지 모델이 알게 합니다.
- **한 번에 하나만 바꾸기.** 빌보드 예시는 장면을 먼저 만든 뒤 날씨만 바꿔서 문구와 레이아웃이 흐트러지지 않게 했습니다.

<a id="menu"></a>
## 📑 목차

- [⭐ 추천](#featured) (6)
- [🔁 GIF 애니메이션](prompts/gif-animation_ko.md) (38) — 동작 하나를 적고 시작 자세로 돌아오게 하며, 카메라는 고정한 짧은 루프입니다.
- [🧩 캐릭터와 스티커](prompts/characters-stickers_ko.md) (12) — 모든 칸에서 같은 캐릭터를 유지하는 스티커 세트, 동작 프레임, 캐릭터 시트.
- [✏️ 이미지 편집과 마크업](prompts/image-editing_ko.md) (14) — 업로드한 이미지에서 한 곳만 바꾸고 나머지는 그대로 두는 프롬프트로, 흔히 원으로 위치를 표시합니다.
- [🔤 포스터와 타이포그래피](prompts/posters-typography_ko.md) (31) — 문구가 정확히 들어가야 하는 포스터, 카드, 빌보드, 로고.
- [📷 인물과 사진](prompts/portrait-photography_ko.md) (34) — 렌즈, 빛, 구도, 피부나 옷감 질감을 촬영 지시서처럼 적은 인물 사진.
- [🎨 일러스트와 3D](prompts/illustration-3d_ko.md) (57) — 그림책, 만화 컷, 종이 공예 장면, 클레이 흉상, 재질 연구.
- [📊 인포그래픽과 UI](prompts/infographics-ui_ko.md) (24) — 라벨까지 정해 둔 도해, 타임라인, 레시피 카드, 슬라이드, 앱 화면.
- [🍱 제품과 음식](prompts/product-food_ko.md) (52) — 상업 촬영처럼 조명한 병, 패키지, 음식.
- [🏙️ 공간과 풍경](prompts/scenes-places_ko.md) (57) — 실내, 건축, 거리, 자연 풍경을 빛 하나와 렌즈 하나로 묶었습니다.
- [❓ 자주 묻는 질문](#faq)
- [🔗 관련 링크](#related)

<a id="featured"></a>
## ⭐ 추천

<a id="gif-animation-01"></a>
### 1. 눈 숲에서 등불 든 원숭이 루프

작성자 [@OpenAI](https://developers.openai.com/api/docs/guides/image-prompting?model=gpt-image-2.6#generate-a-looping-gif) · 2초 · 1:1 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-01#gif-animation-01)** · [원본 게시물](https://developers.openai.com/api/docs/guides/image-prompting?model=gpt-image-2.6#generate-a-looping-gif)

<a href="https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-01#gif-animation-01"><img src="assets/gif/gif-animation-01.gif" width="560" alt="눈 숲에서 등불 든 원숭이 루프 – GPT Image 2.6"></a>

**프롬프트:**

```text
A little monkey in an olive-green hooded coat stands in a snowy pine forest at dusk. A wooden cabin glows in the background. The monkey holds a glowing amber paper lantern at chest height, slowly lifts it, looks up and blinks, then lowers it back to its starting pose. Keep the lantern in its hands and the camera still. Make the motion loop smoothly.
```

<a id="gif-animation-32"></a>
### 30. 뉴욕 스노볼

작성자 [@dreamwieber](https://x.com/dreamwieber) · 1초 · 1:1 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-32#gif-animation-32)** · [원본 게시물](https://x.com/dreamwieber/status/2118190877567037732)

<a href="https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-32#gif-animation-32"><img src="assets/gif/gif-animation-32.gif" width="560" alt="뉴욕 스노볼 – GPT Image 2.6"></a>

**프롬프트:**

```text
generate an animated gif of a beautiful NYC snow globe
```

<a id="gif-animation-15"></a>
### 15. 볼풀에서 노는 클레이 아기 고양이

작성자 [@dreamwieber](https://x.com/dreamwieber) · 1초 · 1:1 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-15#gif-animation-15)** · [원본 게시물](https://x.com/dreamwieber/status/2118191599872344467)

<a href="https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-15#gif-animation-15"><img src="assets/gif/gif-animation-15.gif" width="560" alt="볼풀에서 노는 클레이 아기 고양이 – GPT Image 2.6"></a>

**프롬프트:**

```text
generate an animated gif of a claymation kitten playing in a plastic ball pit
```

<a id="gif-animation-14"></a>
### 14. 자전거 타는 펠리컨

작성자 [@SSHCodes](https://x.com/SSHCodes) · 1초 · 1:1 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-14#gif-animation-14)** · [원본 게시물](https://x.com/SSHCodes/status/2118127375481504100)

<a href="https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-14#gif-animation-14"><img src="assets/gif/gif-animation-14.gif" width="560" alt="자전거 타는 펠리컨 – GPT Image 2.6"></a>

**프롬프트:**

```text
generate a gif of a pelican riding a bicycle
```

<a id="gif-animation-27"></a>
### 25. 커피 내리는 로봇

작성자 [@sousoccer6](https://x.com/sousoccer6) · 2초 · 1:1 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-27#gif-animation-27)** · [원본 게시물](https://x.com/sousoccer6/status/2118210705585537226)

<a href="https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-27#gif-animation-27"><img src="assets/gif/gif-animation-27.gif" width="560" alt="커피 내리는 로봇 – GPT Image 2.6"></a>

**프롬프트:**

```text
コーヒーを淹れるロボット
```

<a id="gif-animation-33"></a>
### 31. 라고스 거리에서 아프로비트 추는 로봇

작성자 [@o_adeeko](https://x.com/o_adeeko) · 1초 · 1:1 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-33#gif-animation-33)** · [원본 게시물](https://x.com/o_adeeko/status/2118203950306410729)

<a href="https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-33#gif-animation-33"><img src="assets/gif/gif-animation-33.gif" width="560" alt="라고스 거리에서 아프로비트 추는 로봇 – GPT Image 2.6"></a>

**프롬프트:**

```text
Create an animated GIF of a robot dancing to Afrobeats on a busy Lagos street. Make the movement loop smoothly.
```

- **[🔁 GIF 애니메이션 전체 38개 보기](prompts/gif-animation_ko.md)**
- **[🧩 캐릭터와 스티커 전체 12개 보기](prompts/characters-stickers_ko.md)**
- **[✏️ 이미지 편집과 마크업 전체 14개 보기](prompts/image-editing_ko.md)**
- **[🔤 포스터와 타이포그래피 전체 31개 보기](prompts/posters-typography_ko.md)**
- **[📷 인물과 사진 전체 34개 보기](prompts/portrait-photography_ko.md)**
- **[🎨 일러스트와 3D 전체 57개 보기](prompts/illustration-3d_ko.md)**
- **[📊 인포그래픽과 UI 전체 24개 보기](prompts/infographics-ui_ko.md)**
- **[🍱 제품과 음식 전체 52개 보기](prompts/product-food_ko.md)**
- **[🏙️ 공간과 풍경 전체 57개 보기](prompts/scenes-places_ko.md)**

<a id="faq"></a>
## ❓ 자주 묻는 질문

<details>
<summary><b>이 GPT Image 2.6 프롬프트는 무료로 써도 되나요?</b></summary>

어떤 프롬프트든 복사하고 고쳐서 실행할 수 있습니다. 프롬프트와 결과물은 카드에 표시된 제작자에게 있으니, 결과 이미지를 상업적으로 쓰기 전에 원문 게시물을 확인하세요.

</details>

<details>
<summary><b>GPT Image 2.6로 GIF는 어떻게 만드나요?</b></summary>

프롬프트를 POST /v1/images/generations로 보내고 output_format을 gif로 설정합니다. frame_count는 2~16프레임(기본 9), frame_duration_ms는 프레임당 20~2000ms(기본 200)이며, 편집 엔드포인트에서는 GIF를 쓸 수 없습니다.

</details>

<details>
<summary><b>GPT Image 2.6 GIF 크기는 어떻게 되나요?</b></summary>

output_format이 gif이면 size는 프레임 한 장의 가로세로이며 auto는 512x512입니다. 모든 프레임이 한 장에 그려지므로 프레임이 클수록 개수가 줄어듭니다. 512x512는 최대 16장, 768x768은 최대 12장입니다.

</details>

<details>
<summary><b>API에서 마크업 편집은 어떻게 하나요?</b></summary>

POST /v1/images/edits에 원본 이미지와 markup을 함께 보냅니다. markup은 원본과 같은 크기로 원이나 메모를 그린 투명 PNG이며, mask와 함께 쓸 수 없습니다.

</details>

<details>
<summary><b>GPT Image 2.6의 complexity 설정은 무엇인가요?</b></summary>

모델이 그리기 전에 얼마나 계획할지를 low, medium, high로 정하며 기본값은 high입니다. quality와 별개이고 따로 과금되지 않습니다. 부분 편집에는 low, 글자가 많거나 레이아웃이 복잡하면 high가 맞습니다.

</details>

<details>
<summary><b>gpt-image-2.6-flare와 gpt-image-2.6-sunburst 중 무엇을 쓰나요?</b></summary>

빠른 반복 작업, 포스터, 제품 이미지는 Flare로 시작하세요. medium이나 high 품질에서 디테일이 부족하거나 반복 편집의 일관성이 더 필요하면 Sunburst로 바꾸세요.

</details>

<details>
<summary><b>GPT Image 2.6에 참고 이미지는 몇 장까지 넣을 수 있나요?</b></summary>

HTTPS 이미지 URL 1~16개입니다. 로컬 파일은 먼저 POST /v1/uploads/images로 업로드해야 합니다.

</details>

<details>
<summary><b>프롬프트는 어떤 언어로 써야 하나요?</b></summary>

여기 프롬프트는 중국어, 일본어, 영어 등 작성자의 원문 그대로이며 번역하지 않았습니다. 그대로 복사하거나 편한 언어로 다시 써도 됩니다.

</details>

<details>
<summary><b>GPT Image 2.6 요금은 어떻게 계산되나요?</b></summary>

결과물마다 사용한 토큰으로 과금됩니다. 품질 단계가 높을수록, GIF 프레임이 많을수록 토큰을 더 씁니다. 현재 요금은 모델 페이지에 있습니다.

</details>

<details>
<summary><b>결과가 카드와 다르게 나오는 이유는 무엇인가요?</b></summary>

이미지 모델은 결과가 고정되지 않아 같은 프롬프트도 매번 다르게 나옵니다. 작성자가 참고 이미지, 다른 설정, 또는 ChatGPT 앱을 썼을 수도 있습니다.

</details>


<a id="related"></a>
## 🔗 관련 링크

- [GPT Image 2.6 프롬프트 · apiko.app](https://apiko.app/ko/gpt-image-2-6-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [GPT Image 2.6 Flare](https://apiko.app/ko/models/gpt-image-2.6-flare?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [GPT Image 2.6 Sunburst](https://apiko.app/ko/models/gpt-image-2.6-sunburst?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [GPT Image 2.5 프롬프트](https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [GPT Image 2 프롬프트](https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [AI 이미지 생성기](https://apiko.app/ko/image-generator?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [APIKO API 코드 예시](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**다른 프롬프트 모음**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts/blob/main/README_ko.md)
- [Awesome Seedance 2.0 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.0-prompts/blob/main/README_ko.md)
- [Awesome Kling 4.0 Prompts](https://github.com/tong0619453646-dev/awesome-kling-4.0-prompts/blob/main/README_ko.md)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts/blob/main/README_ko.md)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts/blob/main/README_ko.md)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts/blob/main/README_ko.md)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts/blob/main/README_ko.md)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts/blob/main/README_ko.md)

<a id="license"></a>
## 📄 라이선스와 출처

프롬프트와 결과물은 각 카드에 표시된 제작자에게 있으며, 카드에서 원문 게시물로 이동할 수 있습니다. fujc683으로 표시된 카드는 awesome-gpt-image-2-6-prompts 저장소의 자료로 CC BY 4.0에 따라 사용합니다. 제목, 설명, 번역, 빌드 스크립트는 [CC BY 4.0](LICENSE)으로 배포합니다. 출처 저장소의 라이선스는 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)에 있습니다.

이 목록이 도움이 됐다면 ⭐ 를 눌러 다른 사람도 찾을 수 있게 해 주세요.
