# FFMPEG: Conversions

## Audio

### Extract an image from an audio file

```bash
ffmpeg -i input.mp3 -an -c:v copy output.jpg
```

### Convert WAV to FLAC

```bash
ffmpeg -i input.wav output.flac
```