Singlish → Sinhala Transliterator — Test Automation Suite
> **Assignment 1 | QA Test Automation**  
> Automated browser-based test runner for the [PixelsSuite Chat Translator](https://www.pixelssuite.com/chat-translator), powered by Playwright and openpyxl.
---
📌 Overview
This project automates the execution of 50 negative test cases that verify the behaviour of a Singlish-to-Sinhala transliteration web application. The script:
Reads test inputs and expected outputs from an Excel workbook (`Assignment 1 - Test cases.xlsx`) 
Opens the target web application in a Chromium browser using Playwright
Types each Singlish input into the UI, triggers transliteration, and captures the actual output
Compares the actual output against the expected output
Writes the result (`PASS` / `FAIL` / `COLLECTED` / `UI Error`) back into the same Excel file 
---
📁 Project Structure
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
🧪 Test Case Summary
The test suite (`Assignment 1 - Test cases.xlsx`, sheet: ` Test cases`) covers 50 negative test cases (`Neg_0001` – `Neg_0050`) across the following input categories:
Category	Examples
Question forms	`oya kawadda enna inne?`
Command forms	`ikmanata enna`, `mata eka denna`
Greetings	`suba dawasak`, `ayubowan yaluwane`
Requests	`karunakarala balanna`
Repeated words	`hari hari ennam`, `tika tika kanna`
Punctuation	`ane! mata denna`, `oya enavada...`
Romanization	`mn oyta kiwwa`, `mama oyta kiyanawa`
English words/phrases	`api on the way inne`, `mama feeling happy`
Digital terms	`wifi password denna`, `zoom eken join wenna`
App names	`whatsapp message ekak`
Acronyms	`ASAP ewanne`, `NIC eka denna`
Clipped forms	`exam ekak thiyenawa`, `lab eke inne`
Place names	`api colombo yanawa`, `kandy trip ekak`
Person names	`kasun awa`, `nimal kiwwa`
Numbers & currency	`100k gaththa`, `Rs 200 denna`, `USD 50`
Time & dates	`7pm enna`, `2026-05-10 meeting`
Units	`5km giya`, `10kg weight`
Slang	`ela machan`, `mara seen ekak`
Online identifiers	`www.google.com balanna`, `abc@gmail.com`
Emojis	`mama sathutin inne 😊`, `eya tharaha 😡`
Each test case records:
Input — Singlish text sent to the UI
Expected Output — Correct Sinhala transliteration
Actual Output — What the application returned
Status — `PASS`, `FAIL`, `COLLECTED`, or `UI Error`
Evidence — Description of the defect observed
---
⚙️ Requirements
System
Python 3.10+
Google Chrome / Chromium (installed automatically by Playwright)
Python Packages
```bash
pip install playwright openpyxl
playwright install chromium
```
---
🚀 How to Run
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
🔧 Configuration Reference
All options can be passed as command-line arguments:
Argument	Default	Description
`--excel`	`test_automation/Assignment 1 - Test cases.xlsx`	Path to the Excel workbook
`--sheet`	` Test cases`	Sheet name inside the workbook
`--url`	`https://www.pixelssuite.com/chat-translator`	URL of the web application under test
`--output`	Same as `--excel`	Output file path for results
`--headless`	`False`	Run browser without a visible UI
`--wait-ms`	`5000`	Wait time (ms) after triggering transliteration
`--retries`	`8`	Number of retries when checking for output
`--retry-wait-ms`	`1000`	Wait between retries (ms)
`--type-delay-ms`	`30`	Delay between keystrokes when typing (ms)
`--timeout-ms`	`60000`	Browser element timeout (ms)
`--slow-mo-ms`	`0`	Slow motion delay for all Playwright actions (ms)
`--save-every`	`0` (disabled)	Save workbook after every N rows
`--keep-open`	`False`	Keep browser open after all rows are processed
`--header-row`	Auto-detected	Override header row index in the sheet
`--input-col`	Auto-detected	Override input column name
`--expected-col`	Auto-detected	Override expected output column name
`--actual-col`	`Actual output`	Column name to write actual results into
`--status-col`	`Status`	Column name to write pass/fail status into
---
📊 Output
After execution, the Excel file is updated in-place (or written to `--output`) with two columns filled in for every processed row:
Actual output — The raw text returned by the application
Status — One of:
`PASS` — Actual output matches expected output exactly
`FAIL` — Actual output does not match expected output
`COLLECTED` — No expected output was provided; actual output was captured for review
`UI Error` — A Playwright interaction error occurred on this row
---
🛠️ How It Works
Excel parsing — The script scans the workbook for the header row using fuzzy column-name matching. It auto-detects columns for input, expected output, actual output, and status — no manual column index configuration needed.
Browser automation — Playwright launches a Chromium instance. The script navigates to the target URL, waits for the page to load, and locates the input and output `<textarea>` elements (identified by their placeholder text: `English` and `Sinhala`).
Input injection — For each test row, the script clears the input textarea thoroughly (using a combination of keyboard shortcuts, `.fill()`, and JavaScript evaluation) before typing the new input. This prevents carry-over from previous tests.
Output capture — After clicking the Transliterate button and waiting, the script reads the output textarea. It retries up to `--retries` times if the output is empty or unchanged from the previous run.
Result writing — The actual output and pass/fail status are written back to the Excel sheet. The file is saved at the end (or incrementally with `--save-every`).
Overlay handling — Cookie consent and acceptance dialogs are automatically dismissed at the start of each test row.
---
📝 Notes
The script targets the chat-translator variant of the PixelsSuite application. Detection is based on the URL containing `chat-translator`.
Merged cells in the Excel sheet are handled gracefully — values are always read from and written to the top-left cell of any merge range.
The `--type-delay-ms` option simulates realistic human typing, which can help with applications that use debounced input handlers.
If the application is slow to respond, increase `--wait-ms` and `--retries`.
---
🤝 Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
---
📄 License
This project is for academic and educational purposes as part of a QA testing assignment.
