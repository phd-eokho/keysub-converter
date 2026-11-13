# keysub-converter

Keysub 자막 ⇔ 한글 대본 변환기

A single-page, offline tool that converts subtitle text between two layouts by copy and paste:

- **Keysub**: SRT-style subtitles, where each entry has a number, a start and end time, and the text.
- **한글**: a tab-indented script, where each entry has a short `MMSS` time stamp, the text, and a `//` line to close it.

## Usage

1. Open `index.html` in a browser. There is nothing to install and no network access is needed.
2. Choose the direction: **Keysub to 한글** or **한글 to keysub**.
3. Paste the source text into its box, press **Transform**, and copy the result from the other box.

## Formats

This on the Keysub side:

```
1
00:01:23,000 --> 00:01:25,500
안녕하세요

2
00:01:26,000 --> 00:01:28,000
첫째 줄
둘째 줄
```

corresponds to this on the 한글 side (the indentation is a tab character):

```
0123	
	안녕하세요
	//
0126	첫째 줄
	둘째 줄
	//
	<끝>
```

- The stamp is the minutes and seconds of the subtitle's start time.
- A one-line subtitle goes on the second row, leaving the first row empty.
- Every entry ends with a `//` row, and the script ends with `<끝>`.

## What is lost in a round trip

The 한글 layout holds less information than the Keysub one, so converting there and back does not reproduce the original timing.

- **Keysub to 한글** keeps only the minutes and seconds of the start time. The hour, the milliseconds and the end time are dropped.
- **한글 to keysub** numbers the entries from 1 and gives each one a one-second span, from `,000` to `,999` of its stamp.
- **Hours** are rebuilt from repeats: the first entry with a given stamp gets hour `00`, the next entry with the same stamp gets `01`, and so on up to `03`.

## License

[MIT](LICENSE)
