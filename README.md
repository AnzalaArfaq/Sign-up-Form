# Sign-up Form

A practice project from [The Odin Project](https://www.theodinproject.com/) — a static
"sign up" page built with plain HTML and CSS. No frameworks, no build step, no
dependencies.

![Sign-up form](signupForm/sign-up-form.png)

## What it is

A two-column sign-up page:

- **Brand column** — a background image with a translucent overlay holding the Odin
  logo and wordmark.
- **Form column** — an intro block and the sign-up form: first name, last name, email,
  phone number (optional), password, and confirm password.

The form posts to `https://www.example.com`, a placeholder. Nothing is actually
submitted anywhere — this is a layout and styling exercise only.

## Project structure

```
.
└── signupForm/
    ├── index.html          # markup for the whole page
    ├── style.css           # all styling
    ├── sign-up-form.png    # screenshot of the finished page
    ├── README.md
    └── assets/
        ├── background.jpg  # background image for the brand column
        ├── odin-lined.png  # Odin logo
        └── norse/          # Norse font (.otf) + its freefont license
```

## Running it

Because the page uses relative paths for the stylesheet and images, open it directly in
a browser:

```bash
open signupForm/index.html
```

Any static server works too, if you prefer one:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/signupForm/
```

## How it's built

Plain CSS, laid out the way you'd expect for this exercise:

- **Flexbox** for the two-column page (`.content-row`) and for the form groups.
- **Grid** for the input area (`.form-grid`), using
  `repeat(auto-fit, minmax(180px, 1fr))` so the fields reflow as space narrows.
- **Custom properties** in `:root` for the color palette and font stack, so retheming
  means editing one block.
- **A local `@font-face`** for the Norse display font, falling back to a sans-serif
  stack for body text.

The inputs use the native `:user-valid` / `:user-invalid` pseudo-classes for green/red
border feedback, and `:focus` for a blue focus ring. Because every field is `required`,
`:user-valid` only fires after a real interaction, so nothing shows red on page load.

## Known rough edges

Left as-is from the in-progress build:

- **Stray attribute** — the password input has a bare `="password"` with no attribute
  name (`signupForm/index.html:83`). Presumably meant to be `autocomplete="password"`.
- **Confirm password is capped at 12 characters** while the password field allows 20, so
  a 13–20 character password can't be confirmed.
- **"Odian" typo** in both the `alt` text and the `<h1>` (`index.html:27,30`).
- **Marketing copy is marked up as `<h2>`** (two of them, `index.html:36,41`). That's body
  copy, not headings — screen readers announce it as a section heading and it pollutes
  the document outline.
- **No mobile breakpoint.** `brand-col` keeps a `min-width: 40%`, so on a phone the image
  column stays a third of a narrow screen while `.form-grid` reflows to one column.
- **Unoptimized images.** `background.jpg` is 1862×2792 and ~1 MB for what renders as a
  cropped background; `sign-up-form.png` is another ~1.2 MB.
- **Missing input affordances** — phone number is `type="text"` (should be `type="tel"`)
  and no field has an `autocomplete` attribute.
- **The form posts to `https://www.example.com`**, so submitting navigates to a
  placeholder site.
- The "Log in" link points at `#`.

## Credits

- Exercise: [The Odin Project](https://www.theodinproject.com/lessons/foundations-recipes-dev-tools/sign-up-form)
- Norse font: included under `signupForm/assets/norse/freefont_license.txt`
