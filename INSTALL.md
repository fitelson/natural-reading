# Install Natural Reading

Natural Reading is an agent skill for converting a URL, PDF, or text into an MP3. Its defaults are Microsoft AndrewNeural (American English) and a relaxed reading pace. It uses Microsoft's online speech service through the third-party `edge-tts` package. An internet connection is required; an API key and the Edge browser are not required. Source text is sent to Microsoft's service. Saved recordings can be played offline.

## Add the skill to Codex

Extract the ZIP so its `natural-reading` folder is inside your Codex skills directory: `$CODEX_HOME/skills`, or `~/.codex/skills` when `CODEX_HOME` is unset. The resulting entrypoint should be `~/.codex/skills/natural-reading/SKILL.md` under the default location. Preserve any existing skill of the same name rather than overwriting it without review.

Start a new Codex task if the skill is not yet listed. Invoke it with a request such as:

> Use $natural-reading to make an MP3 of this PDF.

Or provide a webpage URL or pasted text. You can override the voice, speed, or source page range in the request.

## Dependencies

The package contains instructions for the agent, not a standalone converter or bundled speech models. It needs:

- Python and `edge-tts` in an isolated environment.
- FFmpeg (including `ffprobe`) for the default pacing and audio verification.
- For PDFs: Poppler or `pdfplumber`/`pypdf`; scanned PDFs also need an OCR tool such as Tesseract.
- For webpages: the agent's web tools or an HTML article extractor such as `trafilatura` when needed.

On a Mac with Homebrew, a possible setup is:

```sh
brew install uv ffmpeg poppler
uv tool install edge-tts
```

Install only missing dependencies. If `edge-tts` is not on PATH after installation, use `uv tool update-shell`, then open a new shell. Alternatively, use `pipx install edge-tts` or install it into a Python virtual environment. On other platforms, install FFmpeg and extraction tools using the platform's normal package manager. Optional OCR and extraction libraries need only be installed when the source requires them.

The audio-generation workflow has been exercised on macOS. Windows and Linux are not yet tested with this skill; playback and installation use host-specific equivalents. The Edge integration depends on a third-party client and may need updates if Microsoft changes its service.

The ZIP includes no API keys, personal documents, voice samples, or machine-specific paths. See `SKILL.md` for the workflow and `references/source-extraction.md` for URL/PDF handling.
