---
name: design-social-photos
description: "Social media image design frameworks covering platform sizes, art direction styles, visual hierarchy rules, and HTML/CSS mockup patterns. Use when designing or planning social media images for any platform. Produces art direction briefs and single-file HTML mockups at exact pixel dimensions."
---

# Social Media Image Design

Frameworks for designing social media images across all major platforms. Produces art direction briefs and HTML/CSS mockups at exact platform dimensions.

## When to Activate

- Designing or planning a social media image, post, or story
- Creating a LinkedIn banner, Instagram post, or YouTube thumbnail
- Writing an art direction brief for social graphics
- Building HTML/CSS mockups for social content
- Reviewing social content for visual best practices

---

## Platform Size Reference

| Platform | Type | Size (px) | Aspect | Notes |
|----------|------|-----------|--------|-------|
| **Instagram** | Post | 1080 × 1080 | 1:1 | Standard feed post |
| **Instagram** | Story/Reel | 1080 × 1920 | 9:16 | Full screen vertical |
| **Instagram** | Carousel | 1080 × 1350 | 4:5 | Portrait in-feed |
| **Facebook** | Post | 1200 × 630 | ~1.9:1 | Link preview / post |
| **Facebook** | Story | 1080 × 1920 | 9:16 | Full screen |
| **Twitter/X** | Post image | 1200 × 675 | 16:9 | Landscape in-feed |
| **Twitter/X** | Card | 800 × 418 | ~1.91:1 | Link card |
| **LinkedIn** | Post | 1200 × 627 | ~1.91:1 | Feed post |
| **LinkedIn** | Article | 1200 × 644 | ~1.86:1 | Article header |
| **Pinterest** | Pin | 1000 × 1500 | 2:3 | Vertical standard |
| **YouTube** | Thumbnail | 1280 × 720 | 16:9 | Video preview |
| **TikTok** | Cover | 1080 × 1920 | 9:16 | Vertical |
| **Threads** | Post | 1080 × 1080 | 1:1 | Same as IG post |

---

## Art Direction Styles

| Style | Best Platforms | Key Elements | Avoid |
|-------|---------------|--------------|-------|
| **Minimalist** | LinkedIn, Twitter | Whitespace, 1-2 colors, clean type | Busy feeds (Instagram) |
| **Bold Typography** | All | Type as hero, high contrast | When brand is visual-first |
| **Gradient Mesh** | Instagram, TikTok | Fluid color transitions, floating elements | When color accuracy matters |
| **Photo-Based** | Instagram, Facebook | Hero image + subtle overlay | When you lack quality photography |
| **Geometric** | LinkedIn, Twitter | Shapes, patterns, structured layout | Casual/lifestyle platforms |
| **Glassmorphism** | Instagram, TikTok | Frosted glass, blur, transparency | Print contexts |
| **Dark Mode / Moody** | Gaming, tech, nightlife | Near-black bg, jewel tones, high contrast | Healthcare, education |
| **Flat Illustration** | Education, health | Custom art, friendly, approachable | When time is limited |
| **Duotone** | Creative, editorial | Two-color photo treatment | When photo is key message |
| **3D / Isometric** | Tech, product | Depth, shadows, modern perspective | Casual/lifestyle content |
| **Retro / Vintage** | Food, craft, heritage | Distressed textures, serif, muted | Modern tech brands |
| **Editorial / Magazine** | LinkedIn, Twitter | Grid layouts, pull quotes, journalistic | Casual social content |

---

## Platform-Specific Best Practices

| Platform | Focus | Text | Colors | Face Rule |
|----------|-------|------|--------|-----------|
| Instagram | Visual-first | Under 20% of image | Strong, saturated | Face close-ups perform well |
| Facebook | Informative | Can have more text | Eye-catching in feed | Warm, relatable imagery |
| Twitter/X | Bold headline | Punchy, 5 words max | High contrast for dark/light mode | Optional |
| LinkedIn | Professional | Thought leadership copy OK | Clean, credibility-forward | Professional headshots |
| Pinterest | How-to / inspirational | Text overlay on images | Bright, discoverable | Lifestyle > headshots |
| YouTube | Click-driving | 3-5 words max | Bright, high contrast | Faces close-up preferred |
| TikTok | Trendy, energetic | Bold, immediate | Youth-oriented, vibrant | Faces work well |

---

## Typography Hierarchy (at 1080px base)

| Element | Min Size | Weight | Notes |
|---------|----------|--------|-------|
| Headline | 48px | Bold (700-900) | Readable at thumbnail size |
| Subheadline | 32px | Semibold (600) | Supporting context |
| Body | 24px | Regular (400) | Supporting detail |
| Caption | 18px | Regular/Light | Use sparingly |
| CTA | 28px | Bold (700) | High contrast, button-like |

Scale proportionally for other platform sizes.

---

## Safe Zone Rules

- Critical content in central **80%** of canvas
- Logo/text: keep 60-80px from edges at 1080px
- Bottom 15%: avoid on Stories (UI elements cover)
- Top 10%: avoid on Stories (avoid status bar overlap)

---

## Color & Contrast

- Minimum WCAG AA contrast ratio: **4.5:1** for all text
- Test designs at 50% size (simulates thumbnail view)
- Consider platform dark/light mode compatibility
- Brand primary color as dominant (60%), secondary as accent (30-40%)

---

## HTML Mockup Template

Single-file HTML at exact platform dimensions. Always inline all CSS.

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=[WIDTH], initial-scale=1.0">
<link href="https://fonts.googleapis.com/css2?family=[FONT]:wght@400;600;700;900&display=swap" rel="stylesheet">
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  html, body {
    width: [WIDTH]px;
    height: [HEIGHT]px;
    overflow: hidden;
    font-family: '[FONT]', system-ui, sans-serif;
  }
  .canvas {
    width: [WIDTH]px;
    height: [HEIGHT]px;
    position: relative;
    background: [COLOR / gradient];
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: [SAFE_ZONE]px;
  }
  .headline {
    font-size: [SIZE]px;
    font-weight: 900;
    color: [COLOR];
    line-height: 1.1;
    letter-spacing: -0.02em;
  }
  .subtext {
    font-size: [SIZE]px;
    color: [COLOR];
    margin-top: 16px;
    max-width: 80%;
  }
  .cta {
    margin-top: 32px;
    background: [COLOR];
    color: [COLOR];
    padding: 16px 40px;
    border-radius: 8px;
    font-size: [SIZE]px;
    font-weight: 700;
  }
  .logo {
    position: absolute;
    top: [SAFE]px;
    left: [SAFE]px;
    font-size: [SIZE]px;
    font-weight: 700;
    color: [COLOR];
  }
</style>
</head>
<body>
  <div class="canvas">
    <div class="logo">[BRAND NAME]</div>
    <div class="headline">[MAIN HEADLINE]</div>
    <div class="subtext">[SUPPORTING TEXT]</div>
    <div class="cta">[CTA TEXT]</div>
  </div>
</body>
</html>
```

### Size Variables by Platform

| Platform / Type | WIDTH | HEIGHT | SAFE_ZONE |
|-----------------|-------|--------|-----------|
| Instagram Post | 1080 | 1080 | 80 |
| Instagram Story | 1080 | 1920 | 120 |
| Instagram Carousel | 1080 | 1350 | 80 |
| Facebook Post | 1200 | 630 | 80 |
| Twitter/X Post | 1200 | 675 | 80 |
| LinkedIn Post | 1200 | 627 | 80 |
| Pinterest Pin | 1000 | 1500 | 80 |
| YouTube Thumbnail | 1280 | 720 | 80 |

---

## Art Direction Brief Template

```
SOCIAL IMAGE BRIEF

PLATFORM: [platform + format, e.g. "Instagram Post (1080x1080)"]
GOAL: [what this image should make the viewer do/feel]

CONTENT
- Headline: [main text, max 7 words]
- Subtext: [supporting message, optional]
- CTA: [action text, if any]
- Brand elements: [logo placement, colors]

STYLE
- Art direction: [style from list above]
- Color palette: [primary + accent, with hex if known]
- Font style: [bold geometric / elegant serif / clean sans / etc.]
- Mood: [3-5 adjectives]

VISUAL ELEMENTS
- Background: [solid / gradient / photo / illustration]
- Supporting graphics: [icons / shapes / texture / none]
- Logo: [top-left / top-right / bottom / none]

PLATFORM NOTES
- [Any platform-specific constraints from the table above]
```

---

## Content-Type Matching

| Content Type | Best Format | Style | Primary Hook |
|-------------|-------------|-------|-------------|
| Thought leadership quote | LinkedIn Post | Editorial / Bold Typography | The quote itself |
| Product launch | Instagram Post + Story | Gradient or Photo-Based | Product visual |
| Event announcement | All platforms | Bold Typography or Geometric | Date + name |
| Case study / stat | LinkedIn, Twitter | Data / Infographic | The number |
| Behind the scenes | Instagram Story | Photo-Based | Authentic moment |
| Educational tip | Pinterest, Instagram | Flat Illustration or Minimalist | Step 1 of N |
| Sale / promotion | Facebook, Instagram | Bold Typography | % or $ savings |
| Job posting | LinkedIn | Corporate Minimal | Role title |
