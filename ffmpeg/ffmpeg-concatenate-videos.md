# FFMPEG: Concatenate videos

Create `input.txt` file in the following format:
```bash
file '/path/to/file1.mp4'
file '/path/to/file2.mp4'
...
```

Run command:
ffmpeg -f concat -safe 0 -i input.txt -c copy concat.mp4
