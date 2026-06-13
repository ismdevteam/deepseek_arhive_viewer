# DeepSeek Archive Viewer

A powerful, self-contained HTML/JS viewer for DeepSeek chat exports (`conversations.json`).  
Works with **100+ MB files** – virtual scrolling, full‑text search, conversation/message navigation, copy to clipboard, and auto‑load of previously used file.

![Screenshot placeholder](screenshot.png) <!-- optional -->

## Features

- 📂 **Load massive JSON exports** – handles 100+ MB files smoothly
- 🔍 **Two‑level search** – global search across all conversations + case‑sensitive in‑chat search (min 3 letters, 1s debounce)
- 🧭 **Message navigation** – Top / Prev / Next / Bottom buttons + arrow keys (↑ ↓) + Home / End
- 📝 **Message numbers** – click any `#42 You` to jump directly to that message
- 📋 **Copy** – copy current message or entire conversation with one click (Ctrl+C / Ctrl+A)
- 🔖 **Bookmarkable URLs** – `?conversation=941&message=204` restores exact position
- 💾 **Auto‑load** – last loaded file is saved in IndexedDB and restored on page reload
- 🎨 **Dark mode** – matches DeepSeek web interface
- 🖥️ **No installation** – just a single HTML file, works offline

## Requirements

- Any modern browser (Firefox, Chrome, Edge, Brave) with **IndexedDB** support (all do)
- No server, no dependencies, no build step.

## Getting Started

### 1. Export your conversations from DeepSeek

1. Log in to [chat.deepseek.com](https://chat.deepseek.com)
2. Click your profile avatar → **Settings**
3. Under **Data** (or **Privacy**), choose **Export data** / **Download conversations**
4. You will receive a `conversations.json` file (it can be >100 MB)

### 2. Download the viewer

Save the HTML file from the [latest release](https://github.com/yourusername/deepseek-archive-viewer/releases) (or clone the repo) – just one file: `deepseek-archive-viewer.html`

### 3. Open the viewer

Double‑click the HTML file, or open it with your browser:  
`File → Open File → deepseek-archive-viewer.html`

### 4. Load your export

Click **📂 Load conversations.json** and select the file you downloaded.  
The viewer will parse it (takes a few seconds for large files) and show all conversations.

**Tip:** After the first load, the file is stored in IndexedDB – the viewer will automatically reload it on next visit.

## Usage

### Navigating conversations

- **Left panel** – list of all conversations (newest first, stable oldest‑first numbering)
- Click any conversation to view its messages
- URL updates with `?conversation=42` (1‑based index)

### Inside a conversation

- **Message numbers** (`#1 You`, `#2 DeepSeek`…) – click to jump to that message
- **Navigation buttons** – Top / Prev / Next / Bottom (or keyboard: ↑ ↓ Home End)
- **Copy current message** – 📋 Copy Msg button (or Ctrl+C when no input focused)
- **Copy entire conversation** – 📚 Copy All button (or Ctrl+A)

### Searching

- **Global search** (top bar) – searches across conversation titles **and** all message content
- **In‑chat search** (inside right panel) – case‑sensitive, minimum 3 letters, 1 second debounce  
  Type a word, then use ← → buttons to jump between matches. Matches are highlighted in yellow, current match in green.

### Bookmarking

- The URL automatically updates with `?conversation=42&message=5` (1‑based indices)
- Share the link or reload the page – the viewer will restore the exact conversation and message

### Adjusting scroll offset

If message labels are hidden behind the top header, open the HTML in a text editor and change:

```js
const SCROLL_OFFSET_PX = 128;  // increase if needed
```

Higher value = message appears lower on screen.

## Keyboard Shortcuts

| Action | Key |
|--------|-----|
| Previous message | ↑ (Up Arrow) |
| Next message | ↓ (Down Arrow) |
| First message | Home |
| Last message | End |
| Copy current message | Ctrl+C (Cmd+C on Mac) |
| Copy entire conversation | Ctrl+A (Cmd+A on Mac) |

*Shortcuts work when no input field is focused.*

## Under the Hood

- **Parsing** – extracts message trees from DeepSeek’s `mapping` structure
- **Virtual scrolling** – only ~20 conversation items are rendered at a time → fast even with 10k+ conversations
- **IndexedDB** – stores the 100+ MB file locally so you don’t reload it manually every time
- **History API** – pushState to keep URL parameters synchronised

## Troubleshooting

### “Parsing large JSON…” takes too long

- First load always takes a few seconds (100 MB file). Subsequent loads from IndexedDB are faster.
- If it hangs, try Firefox – often better at handling huge JSON heaps.

### In‑chat search doesn’t highlight

- Search is **case‑sensitive** and requires **at least 3 characters**
- Wait 1 second after typing – the search is debounced

### Auto‑load doesn’t restore the last file

- Check that your browser doesn’t clear IndexedDB on exit (some private/incognito modes do)
- Try reloading the file manually once – it will overwrite the stored copy

## Contributing

Issues and pull requests are welcome! Please report any bugs or suggest improvements.

## License

**GPLv3** – see [LICENSE](LICENSE) file for details.

## Acknowledgments

- [DeepSeek](https://www.deepseek.com/) – for the great AI chats and structured export
- The viewer uses no external libraries – pure HTML/CSS/JS

---

*Built with ❤️ for DeepSeek users who want to archive and explore their conversations.*
