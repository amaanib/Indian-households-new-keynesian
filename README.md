# imHANKing it: Hand-to-Mouth Households in India (AIDIS Round 77)

Classifying Indian households as **hand-to-mouth (HtM)** or **Ricardian** using the 77th round of the *All India Debt and Investment Survey* (AIDIS, 2019), and comparing a simple liquid-wealth cutoff against the **Kaplan–Violante (2014)** two-asset method.

📄 **[View the rendered report](./aidis77_kv_analysis.html)** — or open the `.html` file directly after cloning.

---

## What's in here

| File | What it is |
|---|---|
| `aidis77_kv_analysis.qmd` | Quarto source — all code, narrative, and figures |
| `aidis77_kv_analysis.html` | Rendered, self-contained report (open in any browser) |
| `kv_final_3panel_map.png` | Liquid-only classification map (3 panels) |
| `kv_final_4panel_map.png` | Kaplan–Violante classification map (4 panels) |
| `README.md` | This file |

---

## The economics, quickly

A **hand-to-mouth household** is one that spends roughly all of its income each period because it holds little liquid wealth — no real cushion for a bad month. This matters because HtM households have a high marginal propensity to consume (MPC), which is central to how fiscal and monetary policy actually transmit through the economy in **HANK-style New Keynesian models** (Kaplan, Moll & Violante, 2018).

We run two classifications:

1. **Liquid-only** — splits households into *Poor HtM*, *Wealthy HtM*, and *Ricardian* based on financial + share assets alone.
2. **Kaplan–Violante (KV)** — adds illiquid wealth (land) as a second dimension, yielding four types: *Poor HtM*, *Illiquid-rich HtM*, *Liquid-rich only*, and *Ricardian (dual asset)*.

The KV map reveals a large group of **"wealthy hand-to-mouth"** households — land-owning but cash-poor — that the simple method misses entirely. In the Indian context this group is huge, and has important implications for policy transmission.

---

## The data

- **Source:** NSS 77th Round, Schedule 18.2 — *All India Debt and Investment Survey (AIDIS)*, collected 2019 by India's National Statistical Office.
- **Blocks used:**
  - **Blocks 1 & 2** — household identifiers, state codes, survey multipliers
  - **Block 9** — land holdings (`b9q2`, `b9q3`, `b9q4`) → illiquid wealth
  - **Block 11a** — financial assets (deposits, bonds, PF) → liquid wealth
  - **Block 11b** — shares & mutual funds → liquid wealth

The raw `.dta` files are **not included** in this repo. You'll need to download them yourself from the [MoSPI AIDIS data portal](https://microdata.gov.in/nada43/index.php/catalog/146).

---

## How to reproduce

### 1. Requirements

- [R](https://cran.r-project.org/) (≥ 4.2)
- [Quarto](https://quarto.org/docs/get-started/) (≥ 1.3)
- R packages:
  ```r
  install.packages(c("haven","dplyr","tidyr","purrr","ggplot2",
                     "sf","rnaturalearth","rmapshaper","patchwork"))
  ```

### 2. Set your data path

Open `aidis77_kv_analysis.qmd` and edit the `data_dir` line near the top:

```r
data_dir <- "path/to/your/Round77sch18pt2Data"
```

### 3. Render

From the terminal:
```bash
quarto render aidis77_kv_analysis.qmd
```

Or in RStudio / Positron: click **Render**.

---

## Key methodological choice: the ₹12,000 threshold

Households are flagged as HtM if their net liquid wealth falls below **₹12,000** — roughly half a month of median household income in India in 2019, following the Kaplan–Violante convention. This is a judgement call; robustness checks at ₹8,000 and ₹15,000 are a natural next step.

---

## References

- Kaplan, G., & Violante, G. L. (2014). *A Model of the Consumption Response to Fiscal Stimulus Payments.* Econometrica, 82(4), 1199–1239.
- Kaplan, G., Moll, B., & Violante, G. L. (2018). *Monetary Policy According to HANK.* American Economic Review, 108(3), 697–743.
- National Statistical Office (2021). *All India Debt and Investment Survey, NSS 77th Round.* Ministry of Statistics and Programme Implementation, Government of India.

---

## License

Code: MIT. The AIDIS microdata is © Government of India and subject to MoSPI's terms of use.
