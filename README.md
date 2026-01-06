# app5-invoice-generation

A small automation tool that converts Excel invoice spreadsheets into nicely formatted **PDF invoices** using Python and FPDF.

## Features
- Scans the `invoices/` folder for all `.xlsx` files.
- Extracts invoice metadata (invoice number and date) from each filename.
- Reads invoice line items from the Excel sheet.
- Generates a tabular PDF invoice for each spreadsheet, including:
  - Product ID
  - Product name
  - Amount purchased
  - Price per unit
  - Total price per line
- Calculates and displays the **total amount** for the invoice.
- Adds a company name and logo to the bottom of each PDF.
- Saves generated PDFs into the `PDFs/` folder.

## Tech Stack
- **Language**: Python 3
- **Libraries**:
  - `pandas` – read Excel files and compute totals
  - `fpdf` – generate PDF files
  - `glob`, `pathlib` – file system utilities

## Project Structure
```text
app5-invoice-generation/
├─ invoices/            # Source Excel invoices (.xlsx)
├─ PDFs/                # Generated PDF invoices
├─ main.py              # Script that performs the conversion
├─ pythonhow.png        # Logo printed on each invoice
└─ README.md
```

## Invoice File Naming Convention
The script expects invoice Excel files in `invoices/` to follow this pattern:

```text
<invoice_number>-<date>.xlsx
```

Examples:
- `10001-2023.1.18.xlsx`
- `10002-2023.1.18.xlsx`

The filename is split on `-` so the first part becomes the invoice number and the second part becomes the date printed in the PDF header.

## Excel Layout Requirements
Each invoice Excel file is read from sheet `"Sheet 1"` and should contain at least the following columns:

- `product_id`
- `product_name`
- `amount_purchased`
- `price_per_unit`
- `total_price`

The script will:
- Use these columns to build the PDF table.
- Sum the `total_price` column to compute the invoice total.

## Installation
Install the required Python packages:

```bash
pip install pandas fpdf
```

## Usage
1. Place your Excel invoice files in the `invoices/` directory following the naming and column conventions above.
2. Ensure a logo image exists at `pythonhow.png` (or update the path in `main.py`).
3. Run the script from the `app5-invoice-generation` folder:

```bash
python main.py
```

4. Open the generated PDF files in the `PDFs/` directory.

## Customization Ideas
- Change fonts, colors, and layout in `main.py` (via FPDF settings) to match your own branding.
- Add customer details (name, address) as extra fields in the Excel file and render them in the PDF header.
- Localize currency symbols / formats, or add tax/VAT breakdowns.
- Wrap the script in a CLI or GUI for non-technical users.
