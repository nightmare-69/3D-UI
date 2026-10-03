# 🧊 3D Tilt Form Card

A pure **HTML + CSS + JavaScript** UI that shows a floating glass-style card with an input field and two buttons. The card tilts in 3D toward your mouse (or finger on mobile) and gently floats on its own. No libraries, no frameworks.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)

## ✨ Features

- 🎬 **Entrance animation**: the card flips in from 3D space when the page loads
- 🌊 **Floating effect**: the card continuously bobs and rotates slightly
- 🖱️ **3D parallax tilt**: the card rotates toward your cursor or touch point
- 🏷️ **Floating label input**: the label slides up and turns green on focus or when text is typed
- 🔘 **Animated buttons**: shine sweep on hover, pulsing green glow on the primary button, and a squish effect on click
- 📱 **Fully responsive**: buttons stack on very small screens, with touch-friendly sizes
- ♿ **Accessible**: visible focus outlines and `prefers-reduced-motion` support

## 📁 Project Structure

```
├── index.html   # Markup + tilt logic (JavaScript)
└── style.css    # All styling, 3D effects and animations
```

## 🧠 How It Works

### 1. 3D Scene Setup
The `.scene` wrapper uses `perspective: 1000px`, which gives depth to everything inside. The `.float` and `.rectangle` elements use `transform-style: preserve-3d`, so their children can sit at different depths.

### 2. Layered Depth
Elements inside the card are pushed out along the Z axis:

| Element    | Depth          |
|------------|----------------|
| Card       | base layer     |
| Input      | `translateZ(40px)` |
| Buttons    | `translateZ(70px)` |

When the card tilts, the buttons move more than the input, which creates a real parallax effect.

### 3. Mouse / Touch Tilt (JavaScript)
The script measures the distance between the pointer and the center of the card, then converts it into rotation values:

```js
card.style.setProperty('--ry', (x * 30) + 'deg');
card.style.setProperty('--rx', (-y * 30) + 'deg');
```

These values go into CSS variables (`--rx`, `--ry`), and the card's `transform` reads them. **Pointer Events** are used, so it works with mouse, touch and pen. When the pointer leaves or lifts, the card resets to flat.

### 4. Two Animations on `.float`
1. `enter` plays once (1.1s) and flips the card into view
2. `float` starts after that and loops forever, giving a gentle hovering motion

### 5. Floating Label Trick
The input uses `placeholder=" "` (a single space). With the CSS selector `input:not(:placeholder-shown) + label`, the label moves up automatically when the user types, with no JavaScript needed. The label's background matches the card color so it appears to "cut" the input border.

### 6. Button Effects
- **Shine**: a `::after` pseudo-element with a skewed gradient sweeps across on hover
- **Glow**: the `.primary` button pulses a green `box-shadow` ring
- **Press**: `:active` scales the button down to `0.95`

## 🎨 Customization

Change the colors from the `:root` block in `style.css`:

```css
:root {
  --page: #1a2332;   /* page background */
  --card: #243247;   /* card color */
  --green: #4cff2a;  /* accent color */
}
```

> ⚠️ If you change `--card`, the label's background updates automatically because it uses the same variable.

Other easy tweaks:
- Tilt strength: change `30` in the JS (higher = more tilt)
- Float speed: change `6s` in the `float` animation
- Pop-out depth: change the `translateZ()` values on `.field` and `.buttons`

## 🚀 Getting Started

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

Then just open `index.html` in your browser. No build step needed.

## 🌐 Browser Support

Works in all modern browsers (Chrome, Edge, Firefox, Safari) that support CSS 3D transforms and Pointer Events.

## 📄 License

MIT. Free to use, modify and share.
