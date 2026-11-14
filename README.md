<div align="center">

<a href="https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-gpt-image-2.6-prompts"><img src="assets/banner.jpg" alt="Awesome GPT Image 2.6 Prompts" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-319_cases-111111)](README.md#menu)
[![Try GPT Image 2.6 on APIKO](https://img.shields.io/badge/Try_GPT_Image_2.6-on_APIKO-4F46E5)](https://apiko.app/models/gpt-image-2.6-flare?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=model_try)
[![GPT Image 2.6 API docs](https://img.shields.io/badge/GPT_Image_2.6-API_docs-111111)](https://apiko.app/docs/api-manual/image-series/gpt-image-2.6-flare/images?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Current-111111)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-%EB%B3%B4%EA%B8%B0-4F46E5)](README_ko.md)

</div>

# Awesome GPT Image 2.6 Prompts

<a id="introduction"></a>
## 🌟 Introduction

**GPT Image 2.6 prompts: 319 copy-ready examples with their results, from looping GIFs and sticker packs to markup edits, posters and product shots.**

GPT Image 2.6 prompts with the image or GIF each one produced: copy one, or send it to the playground and change the details. The GIF results loop right here on GitHub.

Search and filter them on [apiko.app/gpt-image-2-6-prompts](https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=intro).

> [!NOTE]
> Each prompt is kept exactly as its author posted it, so most are in English; titles and descriptions are ours. Every case credits the author and links to the original post.

<a id="quick-start"></a>
## 🚀 Quick start

**In the browser:** every case has a **Run on APIKO** link. It opens the example on [apiko.app](https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=browser); press **Use** there to load the prompt into the GPT Image 2.6 playground.

**With the API:** create an [APIKO API key](https://apiko.app/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=api_key), then create an async task and poll it until the image is ready.

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

Endpoints: `POST https://api.apiko.app/v1/images/generations` (create a task) · `GET https://api.apiko.app/v1/tasks/{id}` (read the status and result)

<a id="how-to-write"></a>
## ✍️ How to write a GPT Image 2.6 prompt

Four structures that recur in the prompts on this page.

- **Looping GIF** · `Subject + one motion + return to the start + fixed camera` — The GIF prompts describe a single action in order, end on the starting pose so the loop closes, and say the camera does not move. Many also name the frame count.
- **Markup edit** · `What is circled + what it becomes + keep the rest` — Draw a circle on the part to change, then write one short instruction per circle. The API takes the drawing as a transparent overlay of the same size.
- **Same character, many images** · `Locked traits + one new pose or scene per image` — Sticker and picture-book prompts list the hair, outfit and colours to keep, then change only the action, the caption or the setting.
- **Photo brief** · `Subject + light + lens or film + texture` — Portrait and product prompts name the light (window light, golden-hour backlight), a lens or film look, and the material detail they want to see.

**What the examples show**

- **Short prompts are enough for a GIF.** Several loops here come from one line, such as a pelican riding a bicycle. Longer prompts add the order of the motion and what must stay still.
- **Write the reply text into the sticker.** Sticker prompts put the caption in quotes and say where it sits, so a set of reactions can share one character.
- **Leave blanks in a reusable prompt.** Template prompts mark the parts to fill with brackets, such as [object] or [Brand Name], and keep the rest fixed.
- **Number the images you upload.** Edit prompts say "the dog from the second image" or "image 1" so the model knows which picture supplies what.
- **Ask for one change at a time.** The billboard example first renders a scene and then changes only the weather, which keeps the text and layout from drifting.

<a id="menu"></a>
## 📑 Menu

- [⭐ Featured](#featured) (6)
- [🔁 GIF animation](prompts/gif-animation.md) (38) — Short loops described as one motion that returns to its starting pose, with the camera held still.
- [🧩 Characters and stickers](prompts/characters-stickers.md) (12) — Sticker sets, sprite frames and character sheets that keep one character the same in every cell.
- [✏️ Image editing and markup](prompts/image-editing.md) (14) — Prompts that change one part of an uploaded image, often marked with a circle, and leave the rest alone.
- [🔤 Posters and typography](prompts/posters-typography.md) (31) — Posters, cards, billboards and logos where the wording has to come out exactly.
- [📷 Portraits and photography](prompts/portrait-photography.md) (34) — People written like a photo brief: lens, light, framing and skin or fabric texture.
- [🎨 Illustration and 3D](prompts/illustration-3d.md) (57) — Picture books, manga panels, paper-cut scenes, clay busts and material studies.
- [📊 Infographics and UI](prompts/infographics-ui.md) (24) — Diagrams, timelines, recipe cards, slides and app screens with their labels spelled out.
- [🍱 Products and food](prompts/product-food.md) (52) — Bottles, packaging and dishes lit like a commercial shoot.
- [🏙️ Places and landscapes](prompts/scenes-places.md) (57) — Interiors, buildings, streets and landscapes, each tied to one light and one lens.
- [❓ FAQ](#faq)
- [🔗 Related](#related)

<a id="featured"></a>
## ⭐ Featured

<a id="gif-animation-01"></a>
### 1. Lantern monkey looping in a snowy forest

by [@OpenAI](https://developers.openai.com/api/docs/guides/image-prompting?model=gpt-image-2.6#generate-a-looping-gif) · 2s · 1:1 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-01#gif-animation-01)** · [Original post](https://developers.openai.com/api/docs/guides/image-prompting?model=gpt-image-2.6#generate-a-looping-gif)

<a href="https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-01#gif-animation-01"><img src="assets/gif/gif-animation-01.gif" width="560" alt="Lantern monkey looping in a snowy forest – GPT Image 2.6"></a>

**Prompt:**

```text
A little monkey in an olive-green hooded coat stands in a snowy pine forest at dusk. A wooden cabin glows in the background. The monkey holds a glowing amber paper lantern at chest height, slowly lifts it, looks up and blinks, then lowers it back to its starting pose. Keep the lantern in its hands and the camera still. Make the motion loop smoothly.
```

<a id="gif-animation-32"></a>
### 30. New York snow globe

by [@dreamwieber](https://x.com/dreamwieber) · 1s · 1:1 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-32#gif-animation-32)** · [Original post](https://x.com/dreamwieber/status/2118190877567037732)

<a href="https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-32#gif-animation-32"><img src="assets/gif/gif-animation-32.gif" width="560" alt="New York snow globe – GPT Image 2.6"></a>

**Prompt:**

```text
generate an animated gif of a beautiful NYC snow globe
```

<a id="gif-animation-15"></a>
### 15. Clay kitten in a ball pit

by [@dreamwieber](https://x.com/dreamwieber) · 1s · 1:1 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-15#gif-animation-15)** · [Original post](https://x.com/dreamwieber/status/2118191599872344467)

<a href="https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-15#gif-animation-15"><img src="assets/gif/gif-animation-15.gif" width="560" alt="Clay kitten in a ball pit – GPT Image 2.6"></a>

**Prompt:**

```text
generate an animated gif of a claymation kitten playing in a plastic ball pit
```

<a id="gif-animation-14"></a>
### 14. Pelican riding a bicycle

by [@SSHCodes](https://x.com/SSHCodes) · 1s · 1:1 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-14#gif-animation-14)** · [Original post](https://x.com/SSHCodes/status/2118127375481504100)

<a href="https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-14#gif-animation-14"><img src="assets/gif/gif-animation-14.gif" width="560" alt="Pelican riding a bicycle – GPT Image 2.6"></a>

**Prompt:**

```text
generate a gif of a pelican riding a bicycle
```

<a id="gif-animation-27"></a>
### 25. Robot brewing coffee

by [@sousoccer6](https://x.com/sousoccer6) · 2s · 1:1 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-27#gif-animation-27)** · [Original post](https://x.com/sousoccer6/status/2118210705585537226)

<a href="https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-27#gif-animation-27"><img src="assets/gif/gif-animation-27.gif" width="560" alt="Robot brewing coffee – GPT Image 2.6"></a>

**Prompt:**

```text
コーヒーを淹れるロボット
```

<a id="gif-animation-33"></a>
### 31. Robot dancing Afrobeats in Lagos

by [@o_adeeko](https://x.com/o_adeeko) · 1s · 1:1 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-33#gif-animation-33)** · [Original post](https://x.com/o_adeeko/status/2118203950306410729)

<a href="https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.6-prompts&utm_content=gif-animation-33#gif-animation-33"><img src="assets/gif/gif-animation-33.gif" width="560" alt="Robot dancing Afrobeats in Lagos – GPT Image 2.6"></a>

**Prompt:**

```text
Create an animated GIF of a robot dancing to Afrobeats on a busy Lagos street. Make the movement loop smoothly.
```

- **[🔁 All 38 GIF animation cases](prompts/gif-animation.md)**
- **[🧩 All 12 Characters and stickers cases](prompts/characters-stickers.md)**
- **[✏️ All 14 Image editing and markup cases](prompts/image-editing.md)**
- **[🔤 All 31 Posters and typography cases](prompts/posters-typography.md)**
- **[📷 All 34 Portraits and photography cases](prompts/portrait-photography.md)**
- **[🎨 All 57 Illustration and 3D cases](prompts/illustration-3d.md)**
- **[📊 All 24 Infographics and UI cases](prompts/infographics-ui.md)**
- **[🍱 All 52 Products and food cases](prompts/product-food.md)**
- **[🏙️ All 57 Places and landscapes cases](prompts/scenes-places.md)**

<a id="faq"></a>
## ❓ FAQ

<details>
<summary><b>Are these GPT Image 2.6 prompts free to use?</b></summary>

You can copy, edit and run any prompt. The prompts and results belong to the creators credited on each card, so check the original post before reusing a result commercially.

</details>

<details>
<summary><b>How do I make a GIF with GPT Image 2.6?</b></summary>

Send the prompt to POST /v1/images/generations with output_format set to gif. frame_count takes 2 to 16 frames (default 9) and frame_duration_ms 20 to 2000 ms per frame (default 200); GIFs are not available on the edits endpoint.

</details>

<details>
<summary><b>What size is a GPT Image 2.6 GIF?</b></summary>

With output_format gif, size is the width and height of one frame, and auto gives 512x512. All frames are drawn on one sheet, so larger frames allow fewer of them: 512x512 takes up to 16 and 768x768 up to 12.

</details>

<details>
<summary><b>How do markup edits work in the API?</b></summary>

Call POST /v1/images/edits with the source image and a markup URL: a transparent PNG of the same size with your circles or notes drawn on it. Markup cannot be combined with a mask.

</details>

<details>
<summary><b>What is the complexity setting in GPT Image 2.6?</b></summary>

complexity sets how much the model plans before drawing: low, medium or high, with high as the default. It is separate from quality and not billed separately; low suits focused edits and high suits dense text and complex layouts.

</details>

<details>
<summary><b>Should I use gpt-image-2.6-flare or gpt-image-2.6-sunburst?</b></summary>

Start with Flare for fast iteration, posters and product images. Switch to Sunburst when you need more detail or more consistency across repeated edits at medium or high quality.

</details>

<details>
<summary><b>How many reference images can GPT Image 2.6 take?</b></summary>

From 1 to 16 HTTPS image URLs. A local file has to be uploaded first with POST /v1/uploads/images.

</details>

<details>
<summary><b>Which language should I write the prompts in?</b></summary>

The prompts here are shown in the author's original language, including Chinese, Japanese and English, and are not translated. Copy them as they are or rewrite them in the language you prefer.

</details>

<details>
<summary><b>How is GPT Image 2.6 billed?</b></summary>

By the tokens each result uses. Higher quality levels and GIFs with more frames use more tokens; current rates are on the model page.

</details>

<details>
<summary><b>Why does my result look different from the card?</b></summary>

Image models are not deterministic, so the same prompt gives a different result each run. Authors may also have used a reference image, other settings or the ChatGPT app.

</details>


<a id="related"></a>
## 🔗 Related

- [GPT Image 2.6 Prompts · apiko.app](https://apiko.app/gpt-image-2-6-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [GPT Image 2.6 Flare](https://apiko.app/models/gpt-image-2.6-flare?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [GPT Image 2.6 Sunburst](https://apiko.app/models/gpt-image-2.6-sunburst?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [GPT Image 2.5 prompts](https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [GPT Image 2 prompts](https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [AI image generator](https://apiko.app/image-generator?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.6-prompts)
- [Code examples for the APIKO API](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**More prompt collections**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts)
- [Awesome Seedance 2.0 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.0-prompts)
- [Awesome Kling 4.0 Prompts](https://github.com/tong0619453646-dev/awesome-kling-4.0-prompts)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts)
- [Awesome Claude Fable 5.2 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-fable-5.2-video-prompts)
- [Awesome Seedream 5.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedream-5.5-prompts)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts)

<a id="license"></a>
## 📄 License and credits

Prompts and results belong to the creators credited on each card, which links to the original post. Cards credited to fujc683 come from the awesome-gpt-image-2-6-prompts repository under CC BY 4.0. Titles, descriptions, translations and the build scripts are released under [CC BY 4.0](LICENSE). Licenses of the source repositories: [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

If this list saves you time, a ⭐ helps others find it.
