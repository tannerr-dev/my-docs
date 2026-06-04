## **1. Download Every Image on a Page**

Tired of right-clicking one by one?  

```
[...document.images].forEach((img, i) => {
  fetch(img.src)
    .then(res => res.blob())
    .then(blob => {
      const a = document.createElement('a');
      a.href = URL.createObjectURL(blob);
      a.download = `image-${i}.jpg`;
      a.click();
    });
});
```

🖼️ Boom—your gallery’s yours now.

---

## **2. Turn Any Page Into a Rainbow Disco**

Perfect for annoying your coworkers or freaking out your friends.  

```
setInterval(() => {
  document.body.style.backgroundColor =
    `hsl(${Math.floor(Math.random() * 360)}, 100%, 50%)`;
}, 100);
```

🌈 Please use responsibly.

---

## [](http://localhost:6571/reader-mode/page?url=https://dev.to/0x3d_site/10-javascript-scripts-you-should-paste-right-now-iee&uuidkey=121FE7D2-209F-4271-815E-EA491C2EE3C0#3-find-all-password-fields-and-reveal-them)**3. Find All Password Fields and Reveal Them**

Because sometimes… you _are_ the hacker.  

```
[...document.querySelectorAll('input[type="password"]')]
  .forEach(input => input.type = 'text');
```

👀 Oops, did I just expose all passwords?

---

## [](http://localhost:6571/reader-mode/page?url=https://dev.to/0x3d_site/10-javascript-scripts-you-should-paste-right-now-iee&uuidkey=121FE7D2-209F-4271-815E-EA491C2EE3C0#4-make-all-text-on-a-page-editable)**4. Make All Text on a Page Editable**

Yup. Like a mini Notion clone.  

```
document.body.contentEditable = true;
document.designMode = 'on';
```

📝 Go ahead—edit headlines, rewrite articles, prank your friend’s LinkedIn.

---

## [](http://localhost:6571/reader-mode/page?url=https://dev.to/0x3d_site/10-javascript-scripts-you-should-paste-right-now-iee&uuidkey=121FE7D2-209F-4271-815E-EA491C2EE3C0#5-play-a-sound-without-any-library)**5. Play a Sound Without Any Library**

Want to blast a beep just because?  

```
new Audio('https://actions.google.com/sounds/v1/cartoon/cartoon_boing.ogg').play();
```

🔊 You can trigger sounds on clicks, keypresses, or chaos.

---

## [](http://localhost:6571/reader-mode/page?url=https://dev.to/0x3d_site/10-javascript-scripts-you-should-paste-right-now-iee&uuidkey=121FE7D2-209F-4271-815E-EA491C2EE3C0#6-auto-scroll-a-page-like-its-reading-to-you)**6. Auto Scroll a Page Like It’s Reading to You**

Just sit back and relax.  

```
setInterval(() => {
  window.scrollBy(0, 5);
}, 50);
```

📖 Feels like magic when paired with speech synthesis.

---

## [](http://localhost:6571/reader-mode/page?url=https://dev.to/0x3d_site/10-javascript-scripts-you-should-paste-right-now-iee&uuidkey=121FE7D2-209F-4271-815E-EA491C2EE3C0#7-convert-any-pages-text-into-speech)**7. Convert Any Page’s Text into Speech**

Okay, this one’s genuinely useful.  

```
const msg = new SpeechSynthesisUtterance(document.body.innerText.slice(0, 500));
speechSynthesis.speak(msg);
```

🗣️ The web… _talks back now._

---

## [](http://localhost:6571/reader-mode/page?url=https://dev.to/0x3d_site/10-javascript-scripts-you-should-paste-right-now-iee&uuidkey=121FE7D2-209F-4271-815E-EA491C2EE3C0#8-highlight-all-links-that-go-to-external-sites)**8. Highlight All Links That Go to External Sites**

Click smart.  

```
[...document.links].forEach(link => {
  if (!link.href.includes(location.hostname)) {
    link.style.backgroundColor = 'yellow';
  }
});
```

⚠️ This is great for SEO, audits, or nosy curiosity.

---

## [](http://localhost:6571/reader-mode/page?url=https://dev.to/0x3d_site/10-javascript-scripts-you-should-paste-right-now-iee&uuidkey=121FE7D2-209F-4271-815E-EA491C2EE3C0#9-show-how-many-words-are-on-a-page)**9. Show How Many Words Are on a Page**

Because who has time to count?  

```
alert(document.body.innerText.trim().split(/\s+/).length + ' words on this page.');
```

✍️ Use it on blogs, articles, or to guilt-trip yourself on Reddit.

---

## [](http://localhost:6571/reader-mode/page?url=https://dev.to/0x3d_site/10-javascript-scripts-you-should-paste-right-now-iee&uuidkey=121FE7D2-209F-4271-815E-EA491C2EE3C0#10-print-a-clean-screenshot-of-any-page-without-ads)**10. Print a Clean Screenshot of Any Page Without Ads**

Remove all the clutter first:  

```
[...document.querySelectorAll('header, footer, nav, aside, .ad, [class*="ad"]')].forEach(el => el.remove());
window.print();
```

🖨️ Welcome to print-friendly mode, the chaos edition.
