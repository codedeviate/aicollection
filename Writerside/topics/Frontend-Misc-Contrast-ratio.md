# Contrast ratio

**Contrast ratio** is calculated using the **relative luminance** of two colors, typically a foreground color (text) and a background color. The formula used is based on the **WCAG (Web Content Accessibility Guidelines)** standard.

### Contrast Ratio Formula:
$
\text{Contrast Ratio} = \frac{L_1 + 0.05}{L_2 + 0.05}
$

Where:
- **L₁** = Relative luminance of the lighter color
- **L₂** = Relative luminance of the darker color
- **Luminance values** range from **0 (black)** to **1 (white)**.
- The **+0.05** is added to avoid division by zero.

### How to Calculate Relative Luminance:
The **relative luminance** of an sRGB color is calculated using its **red, green, and blue (RGB)** values, which must first be converted to a linear space using the formula:

$
L = 0.2126 \times R + 0.7152 \times G + 0.0722 \times B
$

Where:
- **R, G, and B** are the gamma-corrected values of the respective color channels.
- If an RGB component value is **≤ 0.03928**, use:
  $
  C_{\text{linear}} = \frac{C}{12.92}
  $
- If an RGB component value is **> 0.03928**, use:
  $
  C_{\text{linear}} = \left(\frac{C + 0.055}{1.055}\right)^{2.4}
  $
- RGB values must be normalized to **0–1** range before calculations.

### Contrast Ratio Guidelines (WCAG 2.1):
- **4.5:1** = Minimum for normal text (small text)
- **3:1** = Minimum for large text (≥18pt or 14pt bold)
- **7:1** = Enhanced contrast for better accessibility
