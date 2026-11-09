# 刻 KIZAMI — lyric timing marker

*crafted by IO/monya*

Tap a key along with a song to place markers, put the lyrics on them,
and export the lyric timing as TSV, SRT, VTT or LRC.

(日本語の説明は README.md にあります。)

Live: https://dev.iomonya.com/kizami/ (just open it in your browser)
License: MIT (LICENSE)

## Getting started
Open `index.html` in a browser. Tested in Chrome and Safari.
KIZAMI is made for a computer with a keyboard. On a phone or tablet, a notice says so (close it to look around).
Songs and lyrics are only read inside your browser. Nothing is sent anywhere.

On Windows, use Ctrl wherever this guide says ⌘.

## Supported files
| Kind | Formats |
|---|---|
| Song | mp3, wav, m4a, aac, flac, ogg, opus |
| Video (only the audio is used) | mp4, m4v, mov, webm |
| Lyrics | txt, md, docx, rtf, html |
| Project file | json |
| Timing | tsv, srt, vtt, lrc |

- The same formats work with the buttons and with drag and drop. Other files are not loaded, and a message tells you so
- For videos, only the audio is taken out; the picture is not used. If the browser cannot read the audio in a video, you will see "Could not read this as audio"
- Size limits: audio and video up to 300 MB and 40 minutes, Word (.docx) up to 30 MB, other text files up to 8 MB

### About lyrics files
- Only the text is loaded. Bold, colors, headings, links, tables and other formatting are dropped. Each table row becomes one line of lyrics
- Both UTF-8 and Shift_JIS text are read correctly
- From Google Docs, use File → Download and save as Word (.docx) or Markdown (.md)
- PDF cannot be loaded. Open the PDF, copy the text, press the pencil button in LYRICS and paste it
- Old Word files (.doc) and Pages documents cannot be loaded. Save or export them as Word (.docx) first
- Ruby (furigana) is not loaded. Text deleted with Word's Track Changes is not loaded either

## How it works
1. Load a song (mp3 etc., or a video) and its lyrics (.txt, .docx etc.). You can also drop the files onto the window
2. Play the song and press `M` where each line starts to place a marker (you can change the key)
3. Select some lyrics and drag them onto a marker in the list on the right or on the waveform
   - You can also select a marker and press `Enter`. The lyrics go in, the next marker is selected, and the cursor moves to the start of the next lyrics, so you can keep going with `⇧End` or `⌥⇧→` then `Enter`
   - Headings such as Intro can simply be skipped
4. If everything is late, fix it all at once with Offset (−1000 to +300 ms). For small shifts, drag a marker on the waveform or use `,` `.`
5. Play the song and check the large text at the top of the screen
6. Choose a format from Export and save it

Notes
- Keys do not work while a Japanese (or other) input method is on. Switch to direct (alphanumeric) input first
- Each song is converted to wav inside the browser before playback, so that times stay exact when you seek in an mp3. The original file is not changed
- With Bluetooth earphones your markers will land late (around 0.5 seconds, depending on the device and connection). Wired earphones or speakers are recommended

## The screen
- Drag the divider between LYRICS and MARKERS to change their sizes. Double-click it to split evenly. On a narrow window, LYRICS goes on top and MARKERS below, and the divider changes their heights
- On a narrow window (under 640 px), the SPEED, KEY and OFFSET labels in the top bar are hidden to save rows. Hover over each control to see what it does
- The ? button at the top right opens the guide as a speech bubble pointing at it, which includes the list of keys. It opens by itself the first time. Click outside it or press `Esc` to close it
- The top buttons are shown as icons (♪ song / lines lyrics / folder open / ▶ play, ❚❚ while playing / down arrow save). Hover over them for a description
- Each row in the marker list has these buttons: ▶ play from just before / eraser make it a "clear the text here" marker (on such a row, T turns it back into a lyric marker) / three boxes split character by character / trash can delete
- Hover over the word MARKERS to see how many markers there are. When two or more are selected, the number selected appears next to the heading
- ◐ at the top right switches the colors: white → black → neon. It starts in white the first time. In black and white, markers differ only in brightness, and only the playhead line has a color (yellow on black, red on white)
- The row under the waveform is also shown as icons (from the left: zoom in, the time-span bar, zoom out / follow the playhead / beat grid: show, metronome, snap, settings / A, B, loop, retake, clear the range (markers stay) / help for the waveform). On the bar, the left end zooms in and the right end shows the whole song; the filled part shows roughly how much is on screen. Buttons that are on have a colored border
- When the window gets narrow, the buttons wrap in groups
- The −/+ and the slider at the right of the LYRICS and MARKERS headings change each text size from 50% to 200%. The middle of the slider is 100%, and dragging moves it in 5% steps. Click the number to go back to 100%
- Hover over a button or slider to see what it does. Hover over the word LYRICS to see how to put lyrics on markers
- EN / JA at the top right switches between English and Japanese. The first time, it follows your browser's language (anything other than Japanese gets English)
- Colors, text sizes and language are kept for next time

## Typing marker text directly
- Click the lyrics cell of a marker in the list to type text directly (for per-character timing, or wording that differs from the lyric sheet)
- `Enter` confirms, `Esc` cancels. Confirming an empty cell turns it back into a marker without lyrics
- Rows with typed text get a ✎

## Editing the lyrics
- The pencil button in LYRICS lets you edit the loaded lyrics in place (line breaks, kana, rewording). The original file is not changed
- ✓ (`⌘Enter`) confirms: placed markers carry over to the edited lyrics, and their text follows the new wording. ✕ (`Esc`) stops editing. While editing, the heading shows "editing"
- Markers that sat on deleted text are kept as typed text (✎). `⌘Z` takes you back to before the edit
- Edited lyrics are included in the autosave and in project files. You can also type or paste lyrics with the pencil button without loading a file

## Beat grid
- **Show** and **Snap** for the beat grid (under the waveform) can be turned on and off separately
- Snap only affects markers placed after you turn it on (`M`, `X`, double-click on the waveform). Existing markers do not move. To move them onto the grid, select them and press `G`
- The snap range is set as "within what % of the finest step" (5–50%, default 25%). At 50%, markers always go to the nearest line
- In Settings, each section has its own first-beat position, BPM (0.01 steps when typed, 0.001 when set from two points), time signature and subdivision
- Where the tempo or time signature changes, add a section with "+ New section at playhead". The first section also shows lines before its first beat (for pickups)
- Set the first beat with "Downbeat at playhead", or drag the section line at the bottom edge of the waveform. If you set it while playing, the Offset is taken into account
- "Fit by two points": calculates the BPM from a first beat and another first beat a given number of bars later
- "Tap tempo": tap along with the song to get a rough BPM (`T` also works while Settings is open)
- Grid settings are saved in the project file too
- Metronome (the button right of Show): clicks on the grid’s beats while playing. Turn it on and off with the button; set the volume, the sound (click, woodblock, beep), “Higher sound on the first beat of each bar” and “Also play subdivisions, softly” in the grid settings. It slows down and speeds up with the playback speed. Metronome settings are kept in the browser, not in the project file

## Measuring your delay
- Click the word "Offset" or the clock button at the top to open the measurement
- Press `M` (your marker key) or `Space` in time with the beeps. You can also click inside the box instead of a key. The first 4 beeps are just for listening
- It measures through the same path as the song (`<audio>`), so the delay of your earphones and of your fingers is measured together
- At the end it asks "Set Offset to ○ ms?". Nothing changes until you press "Apply"

## A–B and retake
- `A` and `B` set A and B at the playhead (you can also hold `⌥` and drag on the waveform). `L` loops A–B
- Drag A or B on the waveform to fine-tune them. Grab the small tag outside each line (A on the left, B on the right) to move it even when a marker is close by. A and B never cross
- `R` (retake): plays from 1.5 seconds before A and moves the markers inside A–B to your new taps, in order. Their lyrics stay with them
  - Extra taps add new markers. If you tap fewer times, the markers left over stay where they were and are selected
  - Playback stops after B. `Esc` or `Space` also stops it. `⌘Z` takes you back to before the retake

## Splitting character by character
- The three-box button in the list (or select a marker and press `S`) breaks that marker's lyrics into pieces
  - "Char": one piece per character. Small kana (ゃ, っ etc.), ー and punctuation join the character before; English words stay whole. A leading "……" or "「" joins the next character
  - "Word": one piece per space-separated word
- The original marker becomes the first piece, and the rest are spread evenly up to the next marker for now. The song then plays from a little before, and each key press moves the next piece to that moment (the same as a retake)
- If you stop partway, the pieces not yet tapped stay where they are and are selected. `⌘Z` takes you back to before the split

## Working with several markers
- Drag across an empty part of the waveform to select the markers in that range (`⇧` adds to the selection). In the list, `⇧`+click selects a range and `⌘`+click selects one at a time. `⌘A` selects all
- Drag the selected markers to move them together. `,` `.` nudge them, `Delete` deletes them, and `G` snaps them to the grid. `Esc` clears the selection

## Exporting and opening
- Choose a format from Export: TSV (for KIZAMI and TOMOJI) / SRT (subtitles for Premiere, YouTube etc.) / VTT (web subtitles) / LRC (synced lyrics)
- In SRT and VTT, each line ends at the next marker. The last line ends 4 seconds after it starts
- The folder button (or drag and drop) opens project files (json) as well as tsv, srt, vtt and lrc. If lyrics are loaded, the text is matched to them; if not, the lyrics are built from the file's text

## Keys
| Key | Action |
|---|---|
| Space | Play / pause |
| M (changeable) | Place a marker here |
| X | Place a "clear the text here" marker |
| Enter | Put the selected lyrics on the selected marker |
| [ ] | Select the previous / next marker |
| , . | Move the selected markers by 10 ms (50 ms with ⇧) |
| P | Play from 1.5 seconds before the selected marker |
| G | Snap the selected markers to the nearest grid line |
| S | Split the selected marker character by character |
| Delete | Delete the selected markers (outside the lyrics pane) |
| A / B | Set A / B at the playhead |
| L | Loop A–B |
| R | Retake A–B |
| ⌘A | Select all markers |
| Esc | Clear the selection, close panels, stop a retake |
| ← → | Back / forward 3 seconds (outside the lyrics pane) |
| ⌘Z / ⇧⌘Z | Undo / redo |
| ⌘S | Save the project file (.json) |

Waveform: click to move the playhead, drag a marker to move it, double-click an empty spot to add a marker, ⌘ + scroll wheel to zoom.

## Saving
- The time of the last autosave is shown at the bottom right of the screen
- Your work is saved in the browser automatically. Load the same song and lyrics (matched by file name) to pick up where you left off
  - It is kept in the browser's storage (localStorage), not as a normal file
  - It is only available in the same browser and profile on the same computer. Clearing your browsing data deletes it. It can hold a few MB
- For a reliable copy, use Save (`⌘S`). It writes `<song>_kizami.json` to your downloads folder. Open it with the folder button to continue on another day, computer or browser. Save at good stopping points

## Security (for anyone hosting it)
- Songs, lyrics and your work are handled only inside the user's browser. The page makes no network requests, and a Content-Security-Policy blocks it from contacting anything outside
- Project files and tsv, srt, vtt and lrc files are fully checked (types and ranges) before use. A crafted file cannot run anything in the page
- Limits: text files 8 MB (Word 30 MB), audio 300 MB and 40 minutes, lyrics 100,000 characters, markers 20,000 (5,000 characters each). Anything beyond that is not loaded, and a message says so
- The autosave never overwrites earlier work before you have been asked whether to restore it. If you decline, the earlier work is kept under another name
- An external audit (Astra) was done on 2026-11-07, and its findings have been addressed (AUDIT_RESPONSE_2026-11-07.md, in Japanese)
- The browser storage used for the autosave can be read by other pages on the same origin. When hosting KIZAMI, keep it on an origin that does not run other people's scripts

## TSV format (`<song>_timing.tsv`)
Tab-separated, UTF-8.

```
start_sec	end_sec	text
20.350	22.420	I was teaching him, reaching in, keeping it crisp,
```

- The Offset is already applied
- end_sec is the time of the next marker (a lyric marker or a clear marker). It is empty on the last line
- Markers without lyrics are not written
- If a marker holds several lines, the line breaks become ` / `

---
crafted by **IO/monya**
