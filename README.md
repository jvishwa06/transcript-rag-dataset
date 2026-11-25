# Transcript RAG Dataset

Scripts that collect YouTube video transcripts and translate Hindi ones into English, producing plain-text documents that can be used as source material for a RAG (Retrieval-Augmented Generation) project. The repo has no RAG code itself.

## Scripts

| File | What it does |
|---|---|
| `main.py` | Downloads transcripts (English or Hindi) for a list of YouTube videos with `youtube-transcript-api` and gets the video titles with `yt-dlp`. It groups the text into 15-second blocks and writes one file per video to `transcripts/`, in the form `[mm:ss] text`. A 5-second delay between requests avoids rate limiting. |
| `hi_en_translate.py` | Translates a Hindi transcript into English with the `ai4bharat/indictrans2-indic-en-dist-200M` model and `IndicTransToolkit`, 8 lines at a time (Hindi `hin_Deva` to English `eng_Latn`). It saves the result next to the input as `<name>_English.txt`. It uses a GPU when available. |

## Included data

`transcripts/` holds the transcripts of four YouTube videos on machine learning and deep learning, plus an English translation of one of them.

## Setup

Requires Python 3.11 or newer.

```bash
pip install youtube-transcript-api yt-dlp transformers==4.53.2 IndicTransToolkit sentencepiece sacremoses
```

The project's `pyproject.toml` lists the complete set of dependencies. The package name there is `livo-extractor`.

## Run

```bash
python main.py              # edit video_urls in the file to choose the videos
python hi_en_translate.py   # set INPUT_FILE at the top of the file first
```

`INPUT_FILE` in `hi_en_translate.py` is a Windows path on the author's machine, so change it to a transcript file of your own.
