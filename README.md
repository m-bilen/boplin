# Boplin

**Learn languages from the subtitles you're already watching.**

Hold Alt, select a word in the subtitles, and Boplin explains what it means *in that scene*, not just in the dictionary. Every word is saved with the line it came from, and a short daily review brings it back before you forget it.

## What it does

- **Catch:** Select any word or line in the subtitles on YouTube, Netflix, Prime Video and HBO Max, and on many other sites whose subtitles are text. The video pauses while you select (you can turn this off).
- **Understand:** Gemini explains the selection in the context of the scene. Idioms and slang are recognised: in *"That question really threw me off"*, "threw off" means *confused me*, not *threw me*.
- **Save:** Words are grouped by show or movie, together with the subtitle line and the moment in the video where you found them.
- **Review:** A multiple-choice quiz shows the original subtitle line and asks what the word means there. Scheduling is based on the SM-2 spaced repetition algorithm, with a daily goal of 20 reviews so the count never piles up.

It works with languages that separate words with spaces (tested with English, Russian and Turkish), and explains in the language you choose.

## Getting started

1. Install Boplin from the [Chrome Web Store](https://chromewebstore.google.com/detail/odfkanmemdikbdihblfnccagifgajpia), or load it from source (see below).
2. Get a free Gemini API key from [Google AI Studio](https://aistudio.google.com/apikey): sign in with your Google account and click **Create API key**. It's free, needs no credit card and takes about a minute. Paste it in Boplin's settings.
3. Play something with subtitles, hold **Alt** (**Option** on Mac) and select a word.

### Load from source

1. Download or clone this repository.
2. Open `chrome://extensions` and turn on **Developer mode**.
3. Click **Load unpacked** and select the project folder.

## Privacy

Your words and settings stay in your browser. The only things that leave it are the text you select and the subtitle line around it, sent to Google Gemini with your own API key. There is no server, no account and no tracking. On the free tier, Google's terms allow it to use what you send to improve its products.

Chrome will warn that Boplin can "read and change data on all websites". It needs this because subtitles can appear on any streaming site, but it only reads text when you hold Alt and select something. Read the full [privacy policy](PRIVACY.md) ([Türkçe](PRIVACY.tr.md)).

## Known limitations

- **Free Gemini keys can be slow or unavailable at peak hours.** Google shares free-tier capacity between all users. A paid key is much more reliable and cheap: roughly 30 cents per 1,000 words at current Flash-Lite prices.
- **Languages without spaces between words** (Japanese, Chinese, Thai) aren't supported yet: selecting part of a line selects the whole line.
- **No export yet.** Your list lives only in this browser and is deleted if you remove the extension. CSV export for Anki is planned.
- **Subtitles must be text.** Subtitles burned into the video image can't be selected.
- **PDFs** opened in Chrome's built-in viewer aren't supported.
- **Linux:** some desktop environments use Alt+drag to move windows, which can get in the way of selecting.
- **Opera** has no side panel, so Boplin opens in a separate window there.
- **All-caps subtitles** are lowercased, so names written in capitals lose their capital letter.

## How it works

Boplin is a Manifest V3 Chrome extension written in plain JavaScript, with no build step and no dependencies.

| File | Role |
| --- | --- |
| `content.js` | Runs on every page, turns on selection mode while Alt is held, expands partial selections to whole words and finds the subtitle line around them |
| `sidepanel.js` | The word list, sessions and header |
| `ai.js` | Builds the prompt and talks to the Gemini API, with timeouts and error handling |
| `analysis.js` | Parses Gemini's answer into the basic meaning, the meaning in the scene and common usages |
| `review.js` / `srs.js` | The review quiz and the SM-2 scheduling |
| `storage.js` | All reads and writes to `chrome.storage.local`, through a write queue so quick selections never overwrite each other |

## Why "Boplin"?

It's a made-up word. To *bop* is to tap something lightly, which is all you do here: a quick tap on a word in the subtitles. The yellow dot in the logo is a **cue mark**, the small dot that flashes in the corner of a film frame to tell the projectionist a reel change is coming.

## License

[MIT](LICENSE)

---

Made by [Mehmet Bilen](https://github.com/m-bilen)