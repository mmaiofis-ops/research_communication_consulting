# How to Change the Hero Button Color

This applies to the "What I CAN HELP YOU WITH:" button on the homepage.

To change its color, update **3 files** (files 1 and 2 affect the live site; file 3 only matters if you recompile the CSS with Gulp):

---

## 1. `css/agency.min.css` — line 7

Find and replace in the minified line:

- `.btn-cta{background-color:#5b9bd5;border-color:#5b9bd5` → replace both `#5b9bd5` with your new color
- `.btn-cta:active,.btn-cta:focus,.btn-cta:hover{background-color:#3d82c0` → replace `#3d82c0` with a slightly darker shade for the hover effect

---

## 2. `css/agency.css` — lines 73–82

```css
/* Normal state — lines 73-75 */
.btn-cta {
  background-color: #5b9bd5;   ← change this
  border-color: #5b9bd5;       ← change this

/* Hover/active state — lines 78-80 */
.btn-cta:active, .btn-cta:focus, .btn-cta:hover {
  background-color: #3d82c0 !important;   ← change this
  border-color: #3d82c0 !important;       ← change this
```

---

## 3. `scss/_global.scss` — lines 65–74 (only if recompiling)

```scss
/* Normal state — lines 65-68 */
.btn-cta {
  background-color: #5b9bd5;   ← change this
  border-color: #5b9bd5;       ← change this

/* Hover/active state — lines 70-72 */
  background-color: #3d82c0 !important;   ← change this
  border-color: #3d82c0 !important;       ← change this
```

---

## Notes

- The two hex values per file should always match (background and border).
- The hover color (`#3d82c0`) should be a darker shade of the main color.
- A quick way to find a darker shade: use [coolors.co](https://coolors.co) or any color picker, take your chosen color, and darken it by ~10–15%.
