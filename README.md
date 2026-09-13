# Natural Reading

A Codex skill that turns webpage URLs, PDFs, pasted text, and text files into faithful spoken narration saved as an MP3. It uses Microsoft Edge voices through the third-party `edge-tts` client. This repository contains agent instructions, not a standalone application or bundled voice models.

## Install and use

Place this repository's `natural-reading` folder in `$CODEX_HOME/skills`, or `~/.codex/skills` when `CODEX_HOME` is unset. Preserve any existing installation before replacing it. See [INSTALL.md](INSTALL.md) for dependency setup and ZIP installation.

The workflow requires Python, `edge-tts`, FFmpeg, and an internet connection. URL and PDF extraction may require additional tools described in the installation guide. Source text is sent to Microsoft's online speech service; saved audio can be played offline. No API key or Edge browser is required.

In Codex, ask:

> Use $natural-reading to make an MP3 of this article: [URL]

> Use $natural-reading to read pages 2–8 of this PDF.

You can also supply pasted text or a text file, and request another voice or pace.

## Defaults

- Voice: `en-US-AndrewNeural` (American English).
- Generate with `python3 -m edge_tts --voice en-US-AndrewNeural` using the Python environment containing the package (or the equivalent `edge-tts` command). Keep the native default rate, volume, and pitch; no tempo processing.
- Preserve wording and order, omitting numeric citation markers during normal article narration.
- Save intermediates in the task's `work/` and final audio in `outputs/`.

See [SKILL.md](SKILL.md) for generation, verification, and delivery, and [source extraction](references/source-extraction.md) for URL and PDF handling.

## Tested scope and limitations

The originating macOS test on September 13, 2026 used `edge-tts` 7.2.8 and a complete webpage article, with the earlier custom pacing settings. Extraction matched the supplied comparison text after normalization of punctuation, spacing, and numeric citation markers. All 2,722 narration-script word tokens matched generated subtitle text. The final MP3 decoded completely and lasted 1,058.8 seconds. These checks establish text coverage and a decodable recording, not perfect pronunciation. That recording predates the switch to native voice defaults; its duration does not describe the current default pace.

PDF extraction and narration are documented but have not yet been exercised. Windows and Linux have not been tested with this skill. The online speech integration may require client updates when Microsoft's service changes.
