# images/

Put photos and pictures here (`.jpg`, `.png`, `.webp`). Keep them under ~500 KB each.

To show one, add it in `index.html` **without** `data-solid`, so it stays in the background
and never blocks the character, e.g. replace the `[ PHOTO ]` placeholder with:

```html
<img src="images/me.jpg" alt="Lucas Caldentey" style="width:220px;height:240px;object-fit:cover">
```

For a pixel-art look add `style="image-rendering:pixelated"` to a small (e.g. 64×64) image.
