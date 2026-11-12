# Sample & Test Files

Free sample files for testing uploads, parsers, players, converters, printers and monitors, in many formats and sizes, no sign-up.
The files are hosted at **[example-file.com](https://example-file.com/en/)**. This repo is an index: [`files.csv`](files.csv) lists every
file with its direct download URL, size in bytes and SHA-256, so tests can download a fixture and check it is the exact file expected.

## Files by format

| Format | What's there | Page |
|---|---|---|
| PDF | Sample PDFs from 1 KB up to 1 GB, for upload limits and viewer tests | [Sample PDF files](https://example-file.com/en/pdf/) |
| Video | MP4, WebM, MOV, MKV in several sizes and resolutions | [Sample video files](https://example-file.com/en/video/) |
| Audio | MP3, WAV, OGG, FLAC, M4A test tones | [Sample audio files](https://example-file.com/en/audio/) |
| Images | JPG, PNG, WebP, HEIC, TIFF | [Sample image files](https://example-file.com/en/image/) |
| Documents | DOCX, XLSX, PPTX | [Sample Office files](https://example-file.com/en/document/) |
| Archives | ZIP, RAR, 7Z, GZ (up to 2 GB) | [Sample archive files](https://example-file.com/en/archive/) |
| Code & data | JSON, XML, YAML, SQL | [Sample code & data files](https://example-file.com/en/code/) |
| Fonts | TTF, OTF, WOFF, WOFF2 | [Sample font files](https://example-file.com/en/font/) |

## Test media for specific jobs

- **Upload testing:** [video files 1 MB–100 MB](https://example-file.com/en/video-for-upload-testing/), [HTML5 video test file](https://example-file.com/en/html5-video-test-file/), [4K test video](https://example-file.com/en/4k-test-video/)
- **A/V checks:** [audio/video sync test](https://example-file.com/en/audio-video-sync-test/), [stereo left/right test](https://example-file.com/en/stereo-left-right-test-video/), [5.1 / 7.1 surround channel test files](https://example-file.com/en/surround-sound-test-files/) (AC-3, E-AC-3, AAC, FLAC, each speaker announced)
- **Monitors & TVs:** [online monitor test](https://example-file.com/en/pc-monitor-setup-tests/), [dead pixel test](https://example-file.com/en/dead-pixel-color-tests/), [UFO / refresh-rate test](https://example-file.com/en/monitor-motion-tests/), [OLED & backlight bleed test](https://example-file.com/en/oled-uniformity-tests/), [projector test patterns](https://example-file.com/en/projector-test-patterns/)
- **Printers:** [printer test page](https://example-file.com/en/printer-test-image/), [color test page](https://example-file.com/en/color-printer-test-page/), [CMYK test chart](https://example-file.com/en/cmyk-printer-test-chart/), [print head alignment](https://example-file.com/en/print-head-test-image/), [inkjet nozzle check](https://example-file.com/en/inkjet-printer-test-image/), [thermal receipt & label printer test](https://example-file.com/en/thermal-printer-test-page/), [A4 test image](https://example-file.com/en/a4-printer-test-image/)

## Use in CI

Every row of `files.csv` is `category,filename,bytes,sha256,url`. Download a fixture and verify it:

```bash
# 10 MB PDF for an upload-limit test
curl -fsSL -o sample.pdf https://cdn.example-file.com/pdf/sample-pdf-10mb.pdf
echo "e0c261aef255c4570976488a801ed26259256bfa628d5d124840aabd5e101e64  sample.pdf" | sha256sum -c -
```

Pick a file by name from the CSV:

```bash
row=$(grep ',sample-pdf-10mb.pdf,' files.csv)
url=$(echo "$row" | cut -d, -f5); sum=$(echo "$row" | cut -d, -f4)
curl -fsSL -o fixture "$url" && echo "$sum  fixture" | sha256sum -c -
```

Cache large fixtures between CI runs instead of downloading them on every build.

## Usage

Files are free to use for testing, development and demos. Please link to the source page instead of re-hosting large files.
Something missing or broken? Open an issue.
