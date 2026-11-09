# 🔬 Histology 205 Reagent Inventory Manager
### *A User Guide for Histotechnologists (SOP 205 v1.0)*

Welcome! This app was built specifically for your histology bench workflow. It replaces the bi-weekly paper clipboard panic, keeps your reagent counts accurate, and ensures no expired bottles ever touch patient tissue.

---

## 📦 1. How Many Items Can It Store?

* **Capacity:** **Over 10,000 to 15,000 reagent items.**
* **How it works:** The app uses your browser’s fast, secure local storage (`localStorage`), which holds up to **5 MB** of data. A single reagent record uses only ~400 bytes.
* **In Perspective:**
  * A typical histology lab tracks **100 to 300** routine stains, special stain components, and solvents.
  * Even a massive hospital pathology core lab running full Immunohistochemistry (IHC) antibody libraries tracks around **1,000 to 2,000** items.
  * **You will never run out of space.** You can add all your routine stains, special stains, IHC antibodies, decalcifiers, fixatives, and paraffin wax supplies with room to spare.
* **Speed:** It runs instantly. Searching and filtering across hundreds of bottles takes less than a millisecond.

---

## 🚀 2. How to Open the App

### Option A: On Your Lab Computer (Zero Setup)
1. Go to the folder:
   `C:\Users\HIER\.gemini\antigravity\scratch\histology-inventory`
2. **Double-click `index.html`**.
3. It will open in Chrome, Edge, or Safari immediately.
4. *Tip:* Bookmark the page in your browser so you can open it with one click anytime! All changes are saved automatically.

### Option B: On Your Phone or Lab iPad (Same Wi-Fi)
If you want to walk around the chemical storage cabinets with your phone or iPad:
1. Open PowerShell or Command Prompt in the folder and type:
   ```bash
   node serve.js
   ```
2. Look at the IP address shown (e.g., `http://192.168.1.50:3000`).
3. Type that into Safari or Chrome on your phone!

---

## 💡 3. The Core Rule: "Stock" vs. "In-Use"

In histology, opened reagents age differently than sealed bottles in the cabinet:

| Term | What It Means | Where It Lives |
| :--- | :--- | :--- |
| **Stock (Sealed)** | Unopened, sealed bottles with factory seals intact. | Flammables cabinet, acid/base cabinet, or $4^\circ\text{C}$ refrigerator. |
| **In-Use (Open)** | The active bottle currently in service. | Staining bench, hood, or automated stainer. |
| **Total** | `Stock + In-Use` | Total volume available in the department. |
| **MIN QTY** | Safety par level. | The minimum quantity needed to avoid halting patient testing. |

---

## 🏷️ 3. Multi-Lot Batch Tracking (Her Exact Example)

In histology, a single reagent often has bottles from **multiple different lots** in storage at the same time:

```
BENCH (IN-USE):
  • 1 bottle  — Lot: 261001 (Exp: 7/31/2027)

STORAGE (SEALED STOCK):
  • (2) bottles — Lot: 249224 (Exp: 3/31/2027) ◄── [⚡ Use Next: Expires First!]
  • (2) bottles — Lot: 261001 (Exp: 7/31/2027)
```

### 1. Opening a Bottle with Multiple Lots:
* When she clicks **`⚡ Open New Bottle`** on an item with multiple lots, the app displays a modal asking:
  * *"Which lot are you opening?"*
  * It automatically highlights and pre-selects the lot that **expires first (FEFO: First-Expired, First-Out)** to keep the lab compliant with CAP/CLIA regulations.
* 1 bottle is deducted from that specific stock lot and moved to the bench with that exact Lot # and expiration date.

### 2. Receiving New Lots:
* When a new box arrives, click **`📦 Receive`**.
* Enter how many bottles, type the new **Lot #**, and choose the **Expiration Date**.
* The new lot is added to that reagent’s stock breakdown.

---

### 3. Visual Liquid Level Gauge (Positioned Below Each Open Bottle):
* Directly below each active in-use bottle on the bench, there is a dedicated liquid level bar:
  * `[ ~100% Full ]` (Fresh bottle)
  * `[ ~50% Left ]` (Plenty remaining / slow-moving)
  * `[ ~25% Low ]` (Getting low)
  * `[ <10% Critical ]` (Nearly dry / urgent reorder)
* **Direct 1-Tap Control:** The font is bold and readable, and she can directly tap any level with gloved fingers to update it instantly.

---

## 🛠️ 4. Everyday Bench Actions (Quick Cheat-Sheet)

```
        ┌────────────────────────────────────────────────────────┐
        │                     DAILY ACTIONS                      │
        └───────────────────────────┬────────────────────────────┘
                                    │
       ┌────────────────────────────┼────────────────────────────┐
       ▼                            ▼                            ▼
⚡ OPEN NEW BOTTLE           ✓ FINISH BOTTLE             📦 RECEIVE SHIPMENT
 Taking 1 sealed bottle       Bottle is empty.            Delivery arrived from
 from cabinet to bench.       Discard or replace          StatLab or Newcomer.
 Stock -1  |  In-Use +1       with fresh bottle.          Stock +N  |  Log new Lot
```

### 1. Taking a New Bottle from the Cabinet $\to$ Bench
* Find the reagent in the app.
* Click **`⚡ Open New Bottle`**.
* **Stock** drops by $1$, **In-Use** goes up by $1$.
* *Smart Alert:* If your remaining total is at or below **MIN QTY**, the card instantly turns red to alert you that it’s time to reorder.

### 2. When an In-Use Bottle Runs Dry
* Click **`✓ Finish`**.
* The app asks: *"Did you pull a replacement from stock now?"*
  * **Click Yes:** It moves a replacement from Stock into In-Use in one step.
  * **Click Cancel/No:** It marks the empty bottle discarded.

### 3. When a Delivery Arrives (Receiving Shipment)
* Click **`📦 Receive`** on that reagent.
* Enter how many bottles arrived (e.g. $+1$, $+2$, $+5$).
* Optional: Type in the new **Lot #** and **Expiration Date**.
* Click **Confirm Restock** — the bottles are added to Stock, and if the item was flagged as "Needs Order", it automatically clears!

### 4. Manually Flagging an Order
* Every card has a shopping cart button (**`🛒`**).
* If you notice a bottle is damaged, leaking, or running low unexpectedly, tap the cart button to immediately add it to the **Needs Order** list.

---

## 🔍 5. Searching & Special Stain Kits

### Searching:
Use the top search bar to type any:
* Reagent name (e.g., `Ferric Chloride`, `Hematoxylin`, `Safron`)
* Catalog / Ref # (e.g., `KC4172`, `1905B`)
* Manufacturer (e.g., `StatLab`, `Newcomer Supply`)
* Lot number (e.g., `255378`)

### Checking Whole Stain Kits:
Special stains often require 5 to 9 reagents to work together. Click the stain pills at the top to filter:
* **Movat Pentachrome (Russell Movat):** All 8 components (Alcian Blue, Alcoholic Hematoxylin, 10% & 2% Ferric Chlorides, Acetic Acid, Phosphotungstic Acid, Safron, Universal Iodine).
* **Trichrome (Masson's):** All 7 components (Weigert's Hematoxylin A & B, Bouin's Fluid, Biebrich Scarlet-Acid Fuchsin, Phosphomolybdic/Phosphotungstic Acid, Aniline Blue, 1% Acetic Acid).
* **Reticulin (Gordon & Sweets):** All 9 components (Solutions A through I: Potassium Permanganate, Oxalic Acid, Ferric Ammonium Sulfate, Silver Nitrate, Ammonium Hydroxide, Sodium Hydroxide, Formalin, Gold Chloride, Sodium Thiosulfate).
* **Gram (Brown-Hopps):** Basic Fuchsin, Cellosolve, Crystal Violet, Gallego's Differentiating, Gram's Iodine, Tartrazine.
* **Jones & GMS Silver:** Silver Nitrate 5%, Sodium Thiosulfate, Gold Chloride, Methenamine-Borax.
* **Congo Red (Amyloid):** Congo Red Solution, Modified Mayer's Hematoxylin, Alkaline Alcohol, 1% Sodium Hydroxide.
* **Giemsa / May-Grunwald:** May-Grunwald Stock, Giemsa Stock, Phosphate Buffer 6.8 pH.
* **Iron (Prussian Blue):** 3% Hydrochloric Acid, 3% Potassium Ferrocyanide, Nuclear Fast Red.
* **Copper (Rhodanine):** Mayer Modified Hematoxylin, Rhodanine Stock, Sodium Borate.
* **AFB (Acid Fast):** 1% Acid Alcohol, Light Green Counterstain, Advanced Carbol Fuchsin.
* **PAS & Diastase:** Alpha Amylase, Schiff Reagent, Periodic Acid.
* **General Lab Reagents:** Glacial Acetic Acid, Periodic Acid 1%, Fast Green.

---

## 🖨️ 6. Bi-Weekly Audit & CAP Binder Printout

Every two weeks when your routine inventory audit is due:
1. Click the green **`🖨️ Bi-Weekly Audit Print`** button in the top bar.
2. The app formats the entire inventory into an official, clean document formatted to **Histology 205 (v1.0)**:
   * **Expiry Date Verified `[✓]`**
   * **Storage Temp Verified `[✓]`**
   * **Stock vs. In-Use breakdown**
   * **Lot & Expiration dates**
   * **Needs Order Placed `[✓]`**
   * **Date Conducted & Performed By**
   * **Supervisor Review Initial & Date line**
3. Print it directly or save it as a PDF for your physical inspection binder.

---

## 💾 7. Data Safety & Backups

* **Automatic Saving:** Everything you do saves instantly in your browser. Even if you restart your computer or close the tab, your data stays intact.
* **Excel Backup:** Click **`💾 Export`** in the top bar anytime. It downloads a clean `.csv` spreadsheet file containing all your reagents, counts, and lot numbers that you can open in Excel or email to your manager.
* **Original Reset:** If you ever want to reset back to the starting spreadsheet data, click the **Reset (`↺`)** button.

---

## ❓ Frequently Asked Questions

**Q: Do I need to be connected to the internet?**  
**A:** No! It works 100% offline. You can use it in basement chemical rooms or sub-basement pathology labs with zero Wi-Fi.

**Q: What if I need to add a brand new reagent?**  
**A:** Click **`+ Add Reagent`** in the top bar, fill in the Name, Ref #, Min Qty, and starting counts, then click Save.

**Q: How do expiration alerts work?**  
* 🔴 **Red Alert:** Expired or expires within 30 days.
* 🟡 **Yellow Alert:** Expires within 60 days.
* 🟢 **Normal:** Healthy shelf life.
