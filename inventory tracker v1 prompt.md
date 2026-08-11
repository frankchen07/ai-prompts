# PRD — OCR Inventory Tracker for Craft Coffee Roastery

## 1. Overview

Build a lightweight inventory tracking workflow that reuses the existing handwritten-chart OCR system.

Instead of manually maintaining a digital inventory sheet, roastery staff:

**Visually inspect inventory → write counts on a standardized sheet → photograph the sheet → verify OCR → submit → inventory updates automatically.**

The system then identifies low-stock items and tells staff what needs to be purchased and where.

## 2. Problem

Inventory at the roastery is currently tracked through visual inspection and handwritten/manual counts.

The existing supplies list contains roughly 40 inventory lines across items such as:

* Cups, lids, sleeves, towels
* Milk and alternative milks
* Matcha, sugar, cocoa, syrups
* Cleaning supplies
* Tanks, growlers, napkins
* Gloves, labels, paper, tape, etc.

Quantities are recorded using inconsistent but human-friendly units such as **boxes, sleeves, packs, bags, bottles, rolls, tanks, and fractional containers** (`1/4 box`, `1 3/4 boxes`, etc.).

This makes maintaining an accurate digital inventory and determining what needs to be purchased unnecessarily manual.

## 3. Goal

Create a simple, low-friction inventory system without changing how employees already perform inventory.

The employee should only need to:

1. Inspect supplies.
2. Write quantities on the inventory sheet.
3. Take a photo.
4. Review OCR results.
5. Confirm.

Everything after confirmation should be automated.

## 4. Core Workflow

**Inventory Sheet → Photo → OCR → Human Verification → Normalize Quantities → Update Inventory → Check Thresholds → Generate Restock Actions**

### OCR + Verification

Reuse the existing OCR pathway to extract:

* Item
* Quantity (unit)
* Date

Before submission, the user can correct OCR mistakes.

### Inventory Normalization

Each inventory item has a configured **base unit and conversion rules**.

Example:

`Milk: 1 box = X individual cartons`

If the employee records `1.5 boxes`, the system can calculate the estimated underlying quantity.

The system should support units such as:

**box / sleeve / pack / bag / bottle / roll / tank / individual item**

and fractional quantities such as:

**¼ / ½ / ¾ / 1½ / 1¾**

### Low-Stock Detection

Each item has a configurable reorder threshold.

The current inventory sheet's rule — **"mark to buy when 1/2 low or 1 sleeve/package down"** — can serve as the starting point, while allowing thresholds to eventually be customized per item.

When inventory falls below the threshold:

**LOW STOCK → Add to Restock List → Display Purchase Location**

Example:

> Almond Milk — LOW
> Current: 1 box
> Restock threshold: 2 boxes
> Buy from: [configured supplier/location]

## 5. Inventory Data Model

Each supply should contain:

**Item Name | Category | Current Quantity | Tracking Unit | Units per Container | Reorder Threshold | Purchase Location | Last Counted**

Purchase locations and conversion rules should be configured once and reused for future scans.

## 6. MVP Screens

Keep the first version extremely small:

**Inventory Dashboard**
Shows current inventory with **OK / LOW** status.

**Scan Inventory**
Upload/take photo → run OCR.

**Verify Scan**
Editable OCR results before submission.

**Restock List**
Only shows items currently requiring purchase, grouped by purchase location where possible.

## 7. Automation

For MVP:

**Confirmed Scan → Update Inventory → Detect Low Stock → Generate Restock List**

Next iteration:

**Low Stock → Calendar reminder/task**

Potential future automation could group purchasing:

> **Costco**
>
> * Milk
> * Almond Milk
> * Paper towels
>
> **Supplier B**
>
> * Cups
> * Lids

This turns inventory counting into an actionable shopping/restocking workflow rather than simply storing quantities.

## 8. MVP Success Criteria

The product succeeds if a staff member can complete an inventory check using only:

**paper + visual inspection + one photo + quick OCR verification**

with no manual spreadsheet entry required.

The key metric for the first version should be:

**Time required to complete inventory + generate an accurate restock list.**

## 9. Out of Scope for V1

Avoid overbuilding the first version.

No need initially for:

* Barcode scanning
* POS integrations
* Automatic consumption forecasting
* Supplier APIs
* Automatic purchasing
* Complex analytics
* Real-time inventory deductions

The core hypothesis to validate is simply:

> **Can OCR turn the roastery's existing handwritten inventory process into a reliable digital inventory and restocking workflow with almost no additional employee effort?**
