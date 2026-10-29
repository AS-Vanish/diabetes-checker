# 🩺 Diabetes Risk Assessment Platform

An interactive, single-page web application that estimates diabetes risk in real time using a **Decision Tree model derived from SPSS output**. Adjust clinical parameters with sliders or numeric inputs and instantly see the model's classification along with the exact decision path that produced it.

> ⚠️ **Disclaimer:** This tool is a statistical simulation for educational and demonstration purposes only. It is **not** a medical device and is **not** a substitute for professional medical diagnosis or advice.

---

## ✨ Features

- **Real-time inference** – results update instantly as inputs change
- **Dual input controls** – synchronized range sliders and numeric fields
- **Radial gauge result card** – clear visual indicator (green = low risk, red = high risk)
- **Decision path visualizer** – step-by-step display of every tree node traversed
- **Reference cards** – quick clinical guidance for Glucose, BMI, and DPF
- **Persian (Farsi) UI with full RTL support** using the Vazirmatn font
- **Responsive, glassmorphism-style design** built with Tailwind CSS
- **Zero build step** – one standalone HTML file, no backend required

---

## 🧬 Input Parameters

| Parameter | Description | Range | Unit |
|-----------|-------------|-------|------|
| **Glucose** | Plasma glucose concentration | 0 – 250 | mg/dL |
| **Age** | Patient age | 10 – 100 | years |
| **BMI** | Body Mass Index | 10.0 – 60.0 | kg/m² |
| **DPF** | Diabetes Pedigree Function (genetic family history score) | 0.000 – 2.500 | index |

These features correspond to those commonly used in the Pima Indians Diabetes dataset.

---

## 🌳 Decision Tree Logic

The classifier is implemented in the `evaluateTree()` function and returns a binary outcome (`0` = Negative, `1` = Positive) together with the traversed path.

```
Glucose ≤ 154
├── Age ≤ 29                      → 0 (Negative)
└── Age > 29
    ├── BMI ≤ 26.7                → 0 (Negative)
    └── BMI > 26.7
        ├── Glucose ≤ 101
        │   ├── DPF ≤ 0.709       → 0 (Negative)
        │   └── DPF > 0.709       → 1 (Positive)
        └── Glucose > 101
            ├── BMI ≤ 43.3
            │   ├── DPF ≤ 0.464   → 0 (Negative)
            │   └── DPF > 0.464   → 1 (Positive)
            └── BMI > 43.3        → 1 (Positive)

Glucose > 154
├── DPF ≤ 0.307
│   ├── DPF ≤ 0.287               → 1 (Positive)
│   └── DPF > 0.287               → 0 (Negative)
└── DPF > 0.307                   → 1 (Positive)
```

---

## 🚀 Getting Started

No installation or build tools are needed.

### Option 1 — Open directly
```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
open index.html        # macOS
# or: start index.html (Windows) / xdg-open index.html (Linux)
```

### Option 2 — Serve locally
```bash
python -m http.server 8000
# then visit http://localhost:8000
```

> An internet connection is required on first load, since Tailwind CSS, Google Fonts, and Lucide Icons are loaded from CDNs.

---

## 🛠️ Tech Stack

- **HTML5 / CSS3 / Vanilla JavaScript**
- [Tailwind CSS](https://tailwindcss.com/) (CDN)
- [Lucide Icons](https://lucide.dev/)
- [Vazirmatn](https://github.com/rastikerdar/vazirmatn) font via Google Fonts
- Inline SVG for the radial gauge

---

## 📁 Project Structure

```
.
├── index.html    # Complete application (markup, styles, logic)
└── README.md
```

---

## 🔧 Customization

- **Update the model:** edit the thresholds and branches inside `evaluateTree(glucose, age, bmi, dpf)`.
- **Change theme colors:** modify the `medical` palette in the `tailwind.config` block.
- **Adjust input ranges:** change the `min` / `max` / `step` attributes on the slider and number inputs.
- **Translate the UI:** all user-facing text lives in `index.html`; the layout is controlled by `dir="rtl"` on the `<html>` tag.

---

## ⚠️ Limitations

- The model is a single decision tree and gives a **binary** output; the gauge does not represent a calibrated probability.
- Accuracy depends entirely on the dataset and SPSS training configuration it was derived from.
- It has not been clinically validated.

---

## 📄 License

Released under the [MIT License](LICENSE). Feel free to use, modify, and distribute.

---

## 🙌 Acknowledgements

- SPSS Decision Tree (CHAID/CART) output used as the basis for the model logic
- Pima Indians Diabetes Database (NIDDK) as the typical feature reference
