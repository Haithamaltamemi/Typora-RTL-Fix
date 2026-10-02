**Note:** This CSS patch is heavily inspired by and extracted from the original [Github-rtl](https://github.com/peleg68/github-rtl) theme. All credit for the "Zero Interference" RTL approach goes to the original author of that theme.

# Typora RTL & Arabic Text Fix

A lightweight, zero-interference CSS patch to fix Right-to-Left (RTL) text direction, mixed-language (Arabic/English) rendering, and code block alignment in [Typora](https://typora.io/).

## The Problem
Default Typora themes often struggle with RTL languages (like Arabic). Common issues include:
- Text displaying Left-to-Right (LTR) instead of RTL.
- Mixed-language text (Arabic + English) appearing in reversed, unreadable order.
- Lists (bulleted/numbered) starting with numbers or English words breaking their alignment.
- Code blocks inheriting RTL direction, making code unreadable.

## The Solution: "Zero Interference" Approach
Unlike other patches that forcefully apply `unicode-bidi: plaintext` to every element (which breaks the native rendering of lists starting with numbers), this patch relies on the **"Zero Interference"** philosophy. 

It sets the base direction of the editor to RTL and adjusts physical paddings/borders, then **leaves the native browser BiDi (Bidirectional) algorithm to handle the text dynamically**. This ensures perfect rendering for pure Arabic, pure English, and complex mixed texts.

## Features
1. **Pure Arabic Text:** Automatically rendered RTL.
2. **Pure English/Foreign Text:** Automatically rendered LTR.
3. **Mixed Text (Arabic + English):** Perfectly aligned RTL, with English words and numbers maintaining their correct logical order without flipping.
4. **Code Blocks:** Strictly forced to LTR and isolated from surrounding RTL text, regardless of the language used inside the code.

## Installation

### Method 1: Apply to ALL Themes (Recommended)
1. Open Typora.
2. Go to **File** > **Preferences** (or `Ctrl + ,` / `Cmd + ,`).
3. Navigate to the **Appearance** section.
4. Click the **"Open Theme Folder"** button.
5. In the opened folder, create a new file named exactly: `base.user.css`
6. Open `base.user.css` with any text editor, paste the CSS code from `typora-rtl-fix.css`, and save.
7. **Restart Typora** completely.

### Method 2: Apply to a Specific Theme
1. Follow steps 1-4 above to open the theme folder.
2. Create a file named `{theme-name}.user.css` (e.g., if your theme is `github.css`, name it `github.user.css`). *Note: Filenames are case-sensitive.*
3. Paste the CSS code, save, and restart Typora.

## How it Works (Technical Details)
- **Base Direction:** `#write { direction: rtl; }` sets the root context.
- **Native BiDi:** By avoiding `unicode-bidi` on `li` and `p` tags, the Chromium engine correctly identifies "Strong" (Arabic/English letters) and "Neutral" (Numbers/Punctuation) characters, aligning lists perfectly even if they start with a number like `1080px`.
- **Isolation:** Code blocks use `direction: ltr` to break out of the RTL context safely.

## Credits
- **Author:** [Haitham Altamemi](https://github.com/Haithamaltamemi)
- **Inspiration:** Based on the layout logic of the `github-rtl` theme, optimized for universal compatibility across all Typora themes.

## License
This project is open-source and available under the [MIT License](LICENSE).
