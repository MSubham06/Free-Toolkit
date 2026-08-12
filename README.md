# Frame Grab

Pull poster frames out of video files and save them as JPEGs, without installing ffmpeg.

One HTML file. Open it in a browser, drop videos in, pick a frame, save. Nothing is uploaded anywhere; every frame is decoded and encoded locally by the browser itself.

## Why this exists

Generating video thumbnails usually means installing ffmpeg and learning its flag syntax, or uploading private footage to an online converter. Neither is appealing when you just need twenty poster frames for a web gallery.

## Use it

Download `frame-grab.html` and open it in Chrome, Edge, Firefox, or Safari. No server, no build step, no internet connection required after download.

1. Drop in your video files, as many as you like
2. Each card shows six suggested frames sampled across the clip
3. Click a suggestion, or drag the slider to any exact moment
4. Save individually, or use Save All to download every selected frame at once

## What it does about black frames

Videos frequently open on a black or blank frame, which makes naive "grab the first frame" tools useless. Frame Grab samples six points spread across each clip, measures the luminance variance of each, and automatically preselects the first one that is not blank. If none of the six work, scrub the slider anywhere you like.

## Output

Filenames match the source, so `v1.mp4` produces `v1.jpg`. The original aspect ratio is preserved, so portrait video gives a portrait thumbnail. This matters for masonry layouts where each tile sizes itself from the image.

Two settings in the toolbar:

- **Max width** caps the long edge in pixels. Height follows the source ratio. Default 720.
- **Quality** is JPEG quality from 40 to 100. Default 82.

## Codec support

The browser has to be able to decode the video, so this works with whatever your browser plays natively. H.264 MP4 is safe everywhere.

H.265 / HEVC, which is what most modern phones record, is **not** supported by Chrome and will show "cannot decode". Convert those to H.264 first using any video editor, then run them through here.

## Browser notes

Chrome asks for permission the first time a page downloads multiple files. Allow it, or the Save All button will only produce the first image.

Large batches are processed one at a time to avoid hitting the browser's concurrent media decoding limit.

## License

MIT. Use it, change it, ship it.
