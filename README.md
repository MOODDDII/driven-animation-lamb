# Driven Animation Lamb

A scroll-driven video experience. The video does not autoplay: scrolling the page scrubs it forward and backward, and a few words fade in over it as you reach them.

**Live:** [https://moodddii.github.io/driven-animation-lamb/](https://moodddii.github.io/driven-animation-lamb/)

## How it works

- The page is a tall section (`400vh`), which gives the scroll distance.
- The `<video>` is `position: sticky` and fills the screen, so it stays in place while you scroll.
- A few lines of JavaScript turn the scroll position into a value from 0 to 1 and write it to `video.currentTime`. Scroll down and the video moves forward, stop and it stops, scroll up and it plays backward.
- Words are absolutely positioned at different heights. Each one is revealed with a pure CSS scroll-driven animation (`animation-timeline: view()`), no JavaScript involved.

## Tech stack

- HTML5 video
- CSS scroll-driven animations
- Vanilla JavaScript
- No dependencies, no build step

## Project structure

```
driven-animation-lamb/
├── index.html
└── assets/
    └── car-edit.mp4
```

The video is 1280×720, 30 fps and about 13 seconds long.

## Browser support

CSS scroll-driven animations (the word reveal) work in Chromium-based browsers (Chrome, Edge) and Safari 26 or newer. In browsers without support the words are shown without the reveal effect. The video scrubbing itself uses plain JavaScript and works everywhere.

## Run locally

Open `index.html` in a browser, or serve the folder over HTTP:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

## Customize

- **Words:** edit the `<span class="text text-N">` elements in `index.html`.
- **Position:** change `top`, `left` and `right` of `.text-0` to `.text-4` in the CSS. Values in `vh` map to the scroll distance.
- **Scroll length:** change the `height` of `.content` (`400vh` by default). A taller section makes the video play slower.
- **Video:** replace `assets/car-edit.mp4`. For smooth backward scrubbing, re-encode the video so that every frame is a keyframe:

```bash
ffmpeg -i input.mp4 -c:v libx264 -g 1 -crf 24 -pix_fmt yuv420p -an -movflags +faststart output.mp4
```

## Deployment

The site is hosted on GitHub Pages, served from the root of the `main` branch.

## Author

[MOODDDII](https://github.com/MOODDDII)
