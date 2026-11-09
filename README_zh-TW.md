<div align="center">

<a href="https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-gpt-image-2.6-prompts"><img src="assets/banner.jpg" alt="Awesome GPT Image 2.6 提示詞" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-319_cases-111111)](README_zh-TW.md#menu)
[![Try GPT Image 2.6 on APIKO](https://img.shields.io/badge/Try_GPT_Image_2.6-on_APIKO-4F46E5)](https://apiko.app/zh-tw/models/gpt-image-2.6-flare?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=model_try)
[![GPT Image 2.6 API docs](https://img.shields.io/badge/GPT_Image_2.6-API_docs-111111)](https://apiko.app/zh-tw/docs/api-manual/image-series/gpt-image-2.6-flare/images?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Default-4F46E5)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-Current-111111)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-%EB%B3%B4%EA%B8%B0-4F46E5)](README_ko.md)

</div>

# Awesome GPT Image 2.6 提示詞

<a id="introduction"></a>
## 🌟 簡介

**GPT Image 2.6 提示詞：319 則可直接複製的範例，附成果圖，包含循環 GIF、貼圖、圈選編輯、海報和商品照。**

每則 GPT Image 2.6 提示詞都附上它產生的圖片或 GIF：直接複製，或送到試用區改幾個細節再跑。 GIF 成品在 GitHub 頁面上直接循環播放。

線上搜尋與篩選： [apiko.app/gpt-image-2-6-prompts](https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=intro).

> [!NOTE]
> 提示詞保持作者發布時的原文，所以大多是英文；標題與簡介由我們撰寫。每則都署名作者並連結原帖。

<a id="quick-start"></a>
## 🚀 快速開始

**網頁上用：** 每則都有「在 APIKO 執行」連結，會在 [apiko.app](https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=browser) 開啟這則範例；點「使用」，提示詞就會填進 GPT Image 2.6 試用台。

**用 API：** 先建立 [APIKO API 金鑰](https://apiko.app/zh-tw/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=api_key)，再建立非同步任務並輪詢，直到圖片生成完成。

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

介面: `POST https://api.apiko.app/v1/images/generations` (建立任務) · `GET https://api.apiko.app/v1/tasks/{id}` (查詢狀態與結果)

<a id="how-to-write"></a>
## ✍️ GPT Image 2.6 提示詞怎麼寫

這些提示詞裡反覆出現的四種結構。

- **循環 GIF** · `主體 + 一個動作 + 回到起點 + 固定鏡頭` — GIF 提示詞依序寫一個動作，結尾回到起始姿勢讓循環接得上，並註明鏡頭不動。不少也會寫出影格數。
- **圈選編輯** · `圈了什麼 + 改成什麼 + 其他不變` — 在要改的地方畫圈，每個圈配一句簡短指令。API 以同尺寸的透明疊加圖接收這些標註。
- **同一角色做多張圖** · `鎖定特徵 + 每張只換動作或場景` — 貼圖和繪本提示詞先列出要保留的髮型、服裝和配色，再只改動作、文字或場景。
- **攝影需求** · `主體 + 光線 + 鏡頭或底片 + 質感` — 人像和商品提示詞會寫出光線（窗光、黃金時刻逆光）、鏡頭或底片感，以及想看到的材質細節。

**從範例看得出什麼**

- **GIF 用短提示詞就夠。** 這裡有好幾則循環動圖只寫了一句話，例如「騎腳踏車的鵜鶘」。長一點的提示詞會補上動作順序和哪些部分不動。
- **把文字寫進貼圖。** 貼圖提示詞把文字放進引號並說明位置，一整套不同情緒的貼圖就能共用一個角色。
- **可重複使用的提示詞要留空格。** 範本類提示詞用方括號標出要填的部分，例如 [object]、[Brand Name]，其他固定不動。
- **替上傳的圖編號。** 編輯類提示詞會寫「第二張圖裡的狗」「圖 1」，讓模型分清楚每張圖提供什麼。
- **一次只改一個地方。** 看板範例先產生場景，再只改天氣，文字和版面就不容易跑掉。

<a id="menu"></a>
## 📑 目錄

- [⭐ 精選](#featured) (6)
- [🔁 GIF 動圖](prompts/gif-animation_zh-TW.md) (38) — 短循環動畫：寫一個動作，最後回到起始姿勢，鏡頭固定不動。
- [🧩 角色與貼圖](prompts/characters-stickers_zh-TW.md) (12) — 貼圖、動作影格和角色設定圖，每一格都是同一個角色。
- [✏️ 圖片編輯與圈選](prompts/image-editing_zh-TW.md) (14) — 只改上傳圖片的其中一處，常用圓圈標出位置，其他維持原樣。
- [🔤 海報與文字排版](prompts/posters-typography_zh-TW.md) (31) — 海報、卡片、看板和 Logo，畫面裡的文字必須一字不差。
- [📷 人像與攝影](prompts/portrait-photography_zh-TW.md) (34) — 照拍攝需求寫人物：鏡頭、光線、取景，以及皮膚或布料的質感。
- [🎨 插畫與 3D](prompts/illustration-3d_zh-TW.md) (57) — 繪本、漫畫分格、紙雕場景、黏土胸像和材質習作。
- [📊 資訊圖表與介面](prompts/infographics-ui_zh-TW.md) (24) — 圖解、時間軸、食譜卡、簡報和 App 介面，標籤都寫清楚。
- [🍱 商品與美食](prompts/product-food_zh-TW.md) (52) — 瓶身、包裝和料理，用商業攝影的方式打光。
- [🏙️ 空間與風景](prompts/scenes-places_zh-TW.md) (57) — 室內、建築、街道和自然風景，每張只搭一種光線和一種鏡頭。
- [❓ 常見問題](#faq)
- [🔗 相關連結](#related)

<a id="featured"></a>
## ⭐ 精選

<a id="gif-animation-01"></a>
### 1. 雪林提燈小猴循環動圖

作者 [@OpenAI](https://developers.openai.com/api/docs/guides/image-prompting?model=gpt-image-2.6#generate-a-looping-gif) · 2 秒 · 1:1 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-01#gif-animation-01)** · [原帖](https://developers.openai.com/api/docs/guides/image-prompting?model=gpt-image-2.6#generate-a-looping-gif)

<a href="https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-01#gif-animation-01"><img src="assets/gif/gif-animation-01.gif" width="560" alt="雪林提燈小猴循環動圖 – GPT Image 2.6"></a>

**提示詞:**

```text
A little monkey in an olive-green hooded coat stands in a snowy pine forest at dusk. A wooden cabin glows in the background. The monkey holds a glowing amber paper lantern at chest height, slowly lifts it, looks up and blinks, then lowers it back to its starting pose. Keep the lantern in its hands and the camera still. Make the motion loop smoothly.
```

<a id="gif-animation-32"></a>
### 30. 紐約雪花水晶球

作者 [@dreamwieber](https://x.com/dreamwieber) · 1 秒 · 1:1 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-32#gif-animation-32)** · [原帖](https://x.com/dreamwieber/status/2118190877567037732)

<a href="https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-32#gif-animation-32"><img src="assets/gif/gif-animation-32.gif" width="560" alt="紐約雪花水晶球 – GPT Image 2.6"></a>

**提示詞:**

```text
generate an animated gif of a beautiful NYC snow globe
```

<a id="gif-animation-15"></a>
### 15. 黏土小貓玩球池

作者 [@dreamwieber](https://x.com/dreamwieber) · 1 秒 · 1:1 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-15#gif-animation-15)** · [原帖](https://x.com/dreamwieber/status/2118191599872344467)

<a href="https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-15#gif-animation-15"><img src="assets/gif/gif-animation-15.gif" width="560" alt="黏土小貓玩球池 – GPT Image 2.6"></a>

**提示詞:**

```text
generate an animated gif of a claymation kitten playing in a plastic ball pit
```

<a id="gif-animation-14"></a>
### 14. 騎腳踏車的鵜鶘

作者 [@SSHCodes](https://x.com/SSHCodes) · 1 秒 · 1:1 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-14#gif-animation-14)** · [原帖](https://x.com/SSHCodes/status/2118127375481504100)

<a href="https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-14#gif-animation-14"><img src="assets/gif/gif-animation-14.gif" width="560" alt="騎腳踏車的鵜鶘 – GPT Image 2.6"></a>

**提示詞:**

```text
generate a gif of a pelican riding a bicycle
```

<a id="gif-animation-27"></a>
### 25. 沖咖啡的機器人

作者 [@sousoccer6](https://x.com/sousoccer6) · 2 秒 · 1:1 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-27#gif-animation-27)** · [原帖](https://x.com/sousoccer6/status/2118210705585537226)

<a href="https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-27#gif-animation-27"><img src="assets/gif/gif-animation-27.gif" width="560" alt="沖咖啡的機器人 – GPT Image 2.6"></a>

**提示詞:**

```text
コーヒーを淹れるロボット
```

<a id="gif-animation-33"></a>
### 31. 拉哥斯街頭跳非洲節拍舞的機器人

作者 [@o_adeeko](https://x.com/o_adeeko) · 1 秒 · 1:1 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-33#gif-animation-33)** · [原帖](https://x.com/o_adeeko/status/2118203950306410729)

<a href="https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-33#gif-animation-33"><img src="assets/gif/gif-animation-33.gif" width="560" alt="拉哥斯街頭跳非洲節拍舞的機器人 – GPT Image 2.6"></a>

**提示詞:**

```text
Create an animated GIF of a robot dancing to Afrobeats on a busy Lagos street. Make the movement loop smoothly.
```

- **[🔁 查看「GIF 動圖」全部 38 則](prompts/gif-animation_zh-TW.md)**
- **[🧩 查看「角色與貼圖」全部 12 則](prompts/characters-stickers_zh-TW.md)**
- **[✏️ 查看「圖片編輯與圈選」全部 14 則](prompts/image-editing_zh-TW.md)**
- **[🔤 查看「海報與文字排版」全部 31 則](prompts/posters-typography_zh-TW.md)**
- **[📷 查看「人像與攝影」全部 34 則](prompts/portrait-photography_zh-TW.md)**
- **[🎨 查看「插畫與 3D」全部 57 則](prompts/illustration-3d_zh-TW.md)**
- **[📊 查看「資訊圖表與介面」全部 24 則](prompts/infographics-ui_zh-TW.md)**
- **[🍱 查看「商品與美食」全部 52 則](prompts/product-food_zh-TW.md)**
- **[🏙️ 查看「空間與風景」全部 57 則](prompts/scenes-places_zh-TW.md)**

<a id="faq"></a>
## ❓ 常見問題

<details>
<summary><b>這些 GPT Image 2.6 提示詞可以免費使用嗎？</b></summary>

提示詞可以自由複製、修改和執行。提示詞與成果歸卡片標示的創作者所有，若要把成果圖用於商業用途，請先看原始貼文。

</details>

<details>
<summary><b>怎麼用 GPT Image 2.6 做 GIF？</b></summary>

把提示詞送到 POST /v1/images/generations，output_format 設為 gif。frame_count 可設 2 到 16 格（預設 9），frame_duration_ms 每格 20 到 2000 毫秒（預設 200）；編輯端點不支援 GIF。

</details>

<details>
<summary><b>GPT Image 2.6 的 GIF 尺寸多大？</b></summary>

output_format 為 gif 時，size 指單一影格的寬高，auto 為 512x512。所有影格畫在同一張圖上，單格越大可用的格數越少：512x512 最多 16 格，768x768 最多 12 格。

</details>

<details>
<summary><b>API 的圈選編輯怎麼用？</b></summary>

呼叫 POST /v1/images/edits，傳入原圖和 markup：一張與原圖同尺寸、畫好圓圈或註記的透明 PNG。markup 不能和 mask 一起使用。

</details>

<details>
<summary><b>GPT Image 2.6 的 complexity 參數是什麼？</b></summary>

complexity 決定模型動筆前要規劃多少，可選 low、medium、high，預設 high。它和 quality 分開設定，也不另外計費；局部編輯適合 low，文字多或版面複雜時用 high。

</details>

<details>
<summary><b>該選 gpt-image-2.6-flare 還是 gpt-image-2.6-sunburst？</b></summary>

先用 Flare，適合快速迭代、海報和商品圖。需要更多細節，或在 medium、high 品質下反覆編輯仍要維持一致時，再換 Sunburst。

</details>

<details>
<summary><b>GPT Image 2.6 最多能放幾張參考圖？</b></summary>

1 到 16 個 HTTPS 圖片網址。本機檔案要先用 POST /v1/uploads/images 上傳。

</details>

<details>
<summary><b>提示詞要用什麼語言寫？</b></summary>

這裡的提示詞保留作者原文，有中文、日文和英文，沒有翻譯。可以直接複製，也可以改寫成你習慣的語言。

</details>

<details>
<summary><b>GPT Image 2.6 怎麼計費？</b></summary>

依每次成果用掉的 token 計費。品質等級越高、GIF 影格越多，用的 token 越多；目前價格請看模型頁。

</details>

<details>
<summary><b>為什麼我跑出來的成果和卡片不一樣？</b></summary>

圖片模型的結果不是固定的，同一則提示詞每次都會不同。作者也可能用了參考圖、其他參數或 ChatGPT 應用程式。

</details>


<a id="related"></a>
## 🔗 相關連結

- [GPT Image 2.6 提示詞 · apiko.app](https://apiko.app/zh-tw/gpt-image-2-6-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [GPT Image 2.6 Flare](https://apiko.app/zh-tw/models/gpt-image-2.6-flare?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [GPT Image 2.6 Sunburst](https://apiko.app/zh-tw/models/gpt-image-2.6-sunburst?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [GPT Image 2.5 提示詞](https://apiko.app/zh-tw/gpt-image-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [GPT Image 2 提示詞](https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [AI 圖片產生器](https://apiko.app/zh-tw/image-generator?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [APIKO API 程式碼範例](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**更多提示詞合集**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts/blob/main/README_zh-TW.md)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts/blob/main/README_zh-TW.md)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts/blob/main/README_zh-TW.md)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts/blob/main/README_zh-TW.md)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts/blob/main/README_zh-TW.md)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts/blob/main/README_zh-TW.md)

<a id="license"></a>
## 📄 授權與出處

提示詞與成果歸每張卡片標示的創作者所有，卡片可連到原始貼文。署名 fujc683 的卡片來自 awesome-gpt-image-2-6-prompts 儲存庫，依 CC BY 4.0 授權使用。標題、簡介、譯文與生成腳本採用 [CC BY 4.0](LICENSE) 授權。來源倉庫的授權條款見 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。

如果這份合集幫你省了時間，按個 ⭐ 能讓更多人看到。
