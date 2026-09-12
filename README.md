# wonderful.today

[English](README.md) | [简体中文](README.zh-CN.md)

## Project Overview

This is a static single-page memorial website designed to showcase the love declaration between Liu Wenlong and Liu Mengting, commemorate their memories, and display the time they have spent together since November 12, 2011. The project is implemented using native HTML, CSS, and jQuery without any build tools, backend services, or frontend framework.

Website: wonderful.today

## Page Content

From top to bottom, the page includes the following sections:

1. **Hero section**: Uses `picture/17.jpg` as the background and displays the names of both people with heart decorations.
2. **Declaration**: Shows words excerpted from the wedding on August 23, 2020, along with the date of signature.
3. **Together Time**: Uses `picture/4.png` as the background and displays the elapsed days, hours, minutes, and seconds since `2011-11-12` in real time.
4. **Footer**: Displays the date when the relationship began and the page's last modified time. The last modified time is generated automatically by the browser using `document.lastModified`.

## Directory Structure

```text
.
├── index.html              # Main page entry and primary content
├── css/
│   ├── base.css            # Reset styles, base typography, and common utility classes
│   ├── bootstrap.css       # Bootstrap grid and base component styles
│   ├── fonts.css           # Lato-Medium and Fontello font definitions
│   └── main.css            # Theme styles, section styling, and responsive rules
├── js/
│   ├── script.js           # Loader animation, background-image setup, and template interaction initialization
│   ├── jquery-1.12.4.min.js
│   ├── jquery.countdown.min.js
│   ├── smooth-scroll.js
│   ├── venobox.min.js
│   └── clipboard.js        # Currently not directly referenced by the entry page
├── fonts/                  # Page fonts and icon font files
└── picture/
    ├── 17.jpg              # Hero background image
    └── 4.png               # Together-time section background image
```

## Running the Project

This is a purely static project, so you can open `index.html` directly in a browser. It is better to serve it through a local static server to get behavior closer to a deployed environment:

```bash
cd wonderful.today
python3 -m http.server 8000
```

Then visit <http://localhost:8000>.

This project does not include a `package.json`, lock file, or build script, so there is no need to run `npm install` or bundle the project.

## Main Implementation Notes

### Background Images

The `.background-img` element inside `index.html` keeps an `<img>` tag. On initialization, `js/script.js` reads its `src`, sets the image as a CSS background, and hides the original `<img>`. The background areas use `background-size: cover` to fill the corresponding sections.

### Loading Animation

The page initially displays a `.loader` overlay. After the window triggers `load`, `script.js` first fades out `.loader-inner`, then fades out the entire loading layer.

### Together Time Counter

The inline script at the bottom of `index.html` uses `2011-11-12` as the start date and recalculates the elapsed time every 500 milliseconds, updating `#elapseClock`. If you want to change the anniversary date, check the footer text `SINCE 2011.11.12` as well.

### Styles and Fonts

- `base.css` provides base resets, typography, and generic utility styles.
- `bootstrap.css` provides the grid layout.
- `main.css` controls the hero section, declaration area, timer section, footer, and responsive behavior.
- `fonts.css` registers the Lato-Medium and Fontello icon fonts; the heart icon uses `.icon-heart`.

## Common Maintenance Entry Points

| Content to modify | File or location |
| --- | --- |
| Modify titles, names, declarations, and footer text | `index.html` |
| Change the start date of the relationship | `index.html` bottom script `var strs` |
| Replace the hero background image | The first `.background-img` image path in `index.html` |
| Replace the timer section background image | The second `.background-img` image path in `index.html` |
| Adjust colors, fonts, spacing, and mobile layout | `css/main.css`, `css/base.css` |
| Adjust loading animation and background-image initialization | `js/script.js` |

## Current Notes

- `js/jquery.countdown.min.js` has been included, but the current timer uses the custom `timeElapse` implementation in `index.html`.
- `js/venobox.min.js` and `js/smooth-scroll.js` are initialized in `script.js`, but the current entry page does not visibly include a photo popup or navigation links with the `.scroll` class.
- `js/clipboard.js` is currently not referenced in `index.html` and is kept as a reserved resource.
- `css/main.css` still contains unused styles from the original wedding template, including event, gallery, gift, guest, and registration form sections. Before removing them, confirm that these modules are not planned to be restored.
- The page depends on local images, fonts, and scripts, so the relative directory structure must remain consistent during deployment.

## Verification Checklist

After making changes, it is recommended to at least check the following:

1. Whether the hero and timer background images display correctly.
2. Whether the loading animation disappears after all resources finish loading.
3. Whether `#elapseClock` continues updating and whether the start date is correct.
4. Whether text, names, and timers overflow on desktop and narrow-screen devices.
5. Whether there are image, font, or script loading errors in the browser developer tools.
