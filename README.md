Singlish → Sinhala Transliterator | Test Automation Suite

Assignment 1 – QA Test Automation

Automated browser-based test runner for the PixelsSuite Chat Translator using Playwright and openpyxl.
Overview
This project runs 50 negative test cases to validate a Singlish-to-Sinhala transliteration web app.

It:

Reads test data from Excel
Automates browser actions
Captures output
Compares results
Writes PASS / FAIL / COLLECTED / UI Error back to Excel
---
Project Structure
```
project-root/
│
├── test_automation/
│   ├── test_automation.py              # Main automation script
│   └── Assignment 1 - Test cases.xlsx # Test case workbook
│
└── README.md
```
---
Test Coverage

Includes 50 negative cases across:

Questions, Commands, Greetings
Slang, Emojis, Acronyms
English phrases, App names
Numbers, Dates, Units
URLs, Emails

Each test contains:

Input
Expected Output
Actual Output
Status
Evidence
Requirements
Python 3.10+
Playwright
openpyxl
```bash
pip install playwright openpyxl
playwright install chromium
```
---
How to Run
Basic run (visible browser, default settings)
```bash
python test_automation/test_automation.py
```
Headless mode (no browser window)
```bash
python test_automation/test_automation.py --headless
```
Custom Excel file and sheet
```bash
python test_automation/test_automation.py \
  --excel "path/to/your/test_cases.xlsx" \
  --sheet " Test cases"
```
Save results to a separate output file
```bash
python test_automation/test_automation.py \
  --output "path/to/results.xlsx"
```
Auto-save after every N rows
```bash
python test_automation/test_automation.py --save-every 5
```
Keep browser open after tests finish
```bash
python test_automation/test_automation.py --keep-open
```
---

---

Output

Excel file updated with:

Actual Output
Status
PASS
FAIL
COLLECTED
UI Error
How It Works
Auto-detects Excel columns
Uses Playwright for browser automation
Clears input before each test
Retries output capture
Writes results back to Excel
Notes
Handles merged Excel cells
Works with PixelsSuite Chat Translator
Adjustable wait & retry settings
Contributing

Pull requests welcome. Open an issue for major changes.
