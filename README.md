# DAY_010 | Scroll Animations

This project is part of the daily code challenge series, **DAY_010**, where I explore an **Awwwards' Site of the Month**. In this project, I recreate a captivating **scroll animation** using **HTML**, **CSS**, **JavaScript**, and **ScrollTrigger**. The design is inspired by the Awwwards element from **Bennett & Clive**'s website. This project showcases how subtle interactions can create a dynamic, visually engaging experience for users.

## Bennett & Clive

Inspired by the scroll-triggered animations seen on **Bennett & Clive's** website.  
Check it out here: [Bennett & Clive](https://bennettandclive.com/)

---

## Inspiration

![Scroll Animations](./assets/DAY_010_2.gif)

## Brands and Layout

This project features a scrolling animation where text dynamically shifts and re-aligns as the user scrolls through a series of brand logos. The text "shoves away" from the central logo as it comes into view, creating a unique, interactive experience.

![Visual Demo](./assets/DAY_010_1.gif)

---

## Project Structure

```bash
DAY_010/
│
├── assets/
│   └── favicon.ico
│   ├── logo1.png
│   ├── miku.gif
│   ├── index_dwn.gif
│   ├── hero.gif
│   └── footer.gif
├── helveticaneue.woff2
├── styles.css
├── index.html
└── script.js
```

---

## Features

- **Scroll-Triggered Animations**: The text dynamically moves away as the logo enters, creating an immersive visual experience.

- **GSAP ScrollTrigger**: This project makes use of **GSAP ScrollTrigger** for smooth and customizable scroll animations.

---

## How to Run

1. **Clone the repository**:

   ```bash
   git clone https://github.com/thounny/DAY_010.git
   ```

2. **Navigate to the project directory**:

   ```bash
   cd DAY_010
   ```

3. **Open the `index.html` file** in your web browser:

   - You can double-click the file in your file explorer, or
   - Serve it using a local development server (e.g., Live Server in VSCode).

---

## How the JavaScript Works

### Scroll-Triggered Animations

The animations are controlled using **GSAP ScrollTrigger**. The central logo grows and the surrounding text pushes away as the user scrolls down the page.

```javascript
document.addEventListener("DOMContentLoaded", function () {
  gsap.registerPlugin(ScrollTrigger);

  const stickyBar = document.querySelector(".sticky-bar");
  const footerTrigger = document.querySelector(".trigger-footer");
  const footerTriggerHeight = footerTrigger.offsetHeight;

  function getStickyBarCenter() {
    return stickyBar.offsetTop + stickyBar.offsetHeight / 2;
  }

  document.querySelectorAll(".row").forEach((row) => {
    ScrollTrigger.create({
      trigger: row,
      start: () => `top+=${getStickyBarCenter() - 550} center`,
      end: () => `top+=${getStickyBarCenter() - 450} center`,
      scrub: true,
      onUpdate: (self) => {
        const progress = self.progress;
        const maxGap = window.innerWidth < 900 ? 10 : 15;
        const minGap = window.innerWidth < 900 ? 0.5 : 1;
        const currentGap = minGap + (maxGap - minGap) * progress;
        row.style.gap = `${currentGap}em`;
      },
    });
  });

  document.querySelectorAll(".row").forEach((row) => {
    ScrollTrigger.create({
      trigger: row,
      start: () => `top+=${getStickyBarCenter() - 400} center`,
      end: () => `top+=${getStickyBarCenter() - 300} center`,
      scrub: true,
      onUpdate: (self) => {
        const progress = self.progress;
        const maxGap = window.innerWidth < 900 ? 0.5 : 1;
        const minGap = window.innerWidth < 900 ? 10 : 15;
        const currentGap = minGap + (maxGap - minGap) * progress;
        row.style.gap = `${currentGap}em`;
      },
    });
  });

  ScrollTrigger.create({
    trigger: footerTrigger,
    start: "top bottom",
    end: () => `top+=${footerTriggerHeight - window.innerHeight} center`,
    scrub: true,
    onUpdate: (self) => {
      const startTop = 50;
      const endTop = 92;
      const newTop = startTop + (endTop - startTop) * self.progress;
      stickyBar.style.top = `${newTop}%`;
    },
  });

  ScrollTrigger.create({
    trigger: footerTrigger,
    start: () =>
      `top+=${footerTriggerHeight - (window.innerHeight + 100)} bottom`,
    end: "bottom bottom",
    scrub: true,
    onUpdate: (self) => {
      const fontSizeStart = window.innerWidth < 900 ? 2.5 : 1.25;
      const fontSizeEnd = 9;
      const newFontSize =
        fontSizeStart + (fontSizeEnd - fontSizeStart) * self.progress;
      stickyBar.querySelectorAll("p").forEach((p) => {
        p.style.fontSize = `${newFontSize}vw`;
      });
    },
  });
});
```

- **ScrollTrigger Setup**: This code listens for the scroll event and adjusts the gap between text elements (left and right) as well as the sticky bar position based on the user’s scroll position.

---

## Technologies Used

- **HTML5**: For structuring the document.
- **CSS3**: For the layout and styling of the project.
- **JavaScript (ES6)**: For handling interactivity and scroll animations.
- **GSAP (GreenSock Animation Platform)**: For creating scroll-triggered animations and visual effects.

---

## Author

![Logo](./assets/index_dwn.gif)

**Thounny Keo**  
Frontend Development Student | Year Up United

---

![miku](./assets/miku.gif)

---
