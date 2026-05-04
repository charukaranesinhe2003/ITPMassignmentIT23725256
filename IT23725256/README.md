# Assignment 1 - Singlish to Sinhala Transliteration Testing

## Overview
This project contains automated test cases for evaluating the accuracy of the Chat Sinhala transliteration function available at [https://www.pixelssuite.com/chat-translator](https://www.pixelssuite.com/chat-translator). The testing focuses on identifying scenarios where the system fails to correctly convert chat-style Singlish input into proper Sinhala output.

## Assignment Details
- **Course**: IT3040 - ITPM (Information Technology Project Management)
- **Assignment**: Option 1 - Transliteration Accuracy Testing
- **Objective**: Test 50 negative test cases covering all 24 Singlish input types
- **Technology**: Playwright automation framework with Python

## Project Structure
```
test_automation/
├── README.md                           # This file
├── Assignment 1 - Test cases.xlsx     # Test cases with results
├── test_automation.py                  # Main Playwright automation script
├── generate_failing_test_cases.py     # Script to generate test cases
├── fill_analysis_columns.py           # Script to analyze input types
└── requirements.txt                    # Python dependencies
```

## Prerequisites
Before running the tests, ensure you have the following installed:

### 1. Python 3.11 or 3.12
Download and install from [python.org](https://www.python.org/downloads/)

### 2. Google Chrome Browser
Download from [google.com/chrome](https://www.google.com/chrome/) (recommended)
*Note: Playwright can also install Chromium automatically*

## Installation & Setup

### Step 1: Clone/Download the Project
```bash
# If using Git
git clone <repository-url>
cd test_automation

# Or extract the provided ZIP file to your desired location
```

### Step 2: Install Python Dependencies
```bash
# Upgrade pip to latest version
pip install -U pip

# Install required packages
pip install playwright openpyxl

# Install Playwright browsers
playwright install
```

### Step 3: Verify Installation
```bash
# Check Python version
python --version

# Check if packages are installed
pip list | grep playwright
pip list | grep openpyxl
```

## Running the Tests

### Automated Test Execution
Run the complete test suite using the following command:

```bash
python test_automation.py --excel "Assignment 1 - Test cases.xlsx" --url "https://www.pixelssuite.com/chat-translator" --wait-ms 5000 --type-delay-ms 80 --slow-mo-ms 200 --save-every 1
```

### Command Line Options
- `--excel`: Path to the Excel file containing test cases
- `--url`: Target website URL for testing
- `--wait-ms`: Wait time after each input (milliseconds)
- `--type-delay-ms`: Delay between keystrokes (milliseconds)
- `--slow-mo-ms`: Slow motion delay for debugging
- `--save-every`: Save results after every N test cases
- `--keep-open`: Keep browser open after completion (for debugging)
- `--headless`: Run in headless mode (no browser UI)

### Example Commands

#### Standard Run (with browser visible)
```bash
python test_automation.py --excel "Assignment 1 - Test cases.xlsx" --url "https://www.pixelssuite.com/chat-translator" --wait-ms 5000 --type-delay-ms 80 --slow-mo-ms 200 --save-every 1
```

#### Headless Run (faster, no browser UI)
```bash
python test_automation.py --excel "Assignment 1 - Test cases.xlsx" --url "https://www.pixelssuite.com/chat-translator" --wait-ms 3000 --type-delay-ms 50 --headless --save-every 5
```

#### Debug Mode (keep browser open)
```bash
python test_automation.py --excel "Assignment 1 - Test cases.xlsx" --url "https://www.pixelssuite.com/chat-translator" --wait-ms 5000 --type-delay-ms 80 --slow-mo-ms 500 --save-every 1 --keep-open
```

## Test Cases

### Coverage
The test suite includes 50 negative test cases covering all 24 Singlish input types:

1. **Question forms** - Questions with Singlish question markers
2. **Command forms** - Imperative sentences and commands
3. **Greetings** - Traditional and casual greetings
4. **Requests** - Polite requests and favors
5. **Responses** - Replies and acknowledgments
6. **Repeated Words** - Duplicated words for emphasis
7. **Inputs with Punctuation Marks** - Various punctuation usage
8. **Romanization/Spelling Variants** - Different spelling approaches
9. **Isolated English Word Insertions** - Single English words in Singlish
10. **Multi-Word English Phrases** - English phrases within Singlish
11. **English Digital Terms** - Technology-related English terms
12. **Platform/App Names** - Social media and application names
13. **English Abbreviations/Acronyms** - Shortened forms and acronyms
14. **English Clipped Forms** - Abbreviated English words
15. **Place Names Embedded** - Geographic locations in Singlish
16. **Person Names Embedded** - Personal names in Singlish context
17. **Numbers and Numeric Suffixes** - Numerical expressions
18. **Currency** - Monetary values and currency symbols
19. **Time Formats** - Time expressions and formats
20. **Dates** - Date formats and expressions
21. **Unit of Measurements** - Measurement units and quantities
22. **Slang and Casual Phrasing** - Informal language and slang
23. **Online Identifiers** - URLs, emails, and web identifiers
24. **Emojis** - Emoji characters and expressions

### Test Case Format
Each test case includes:
- **Test Case ID**: Unique identifier (Neg0001-Neg0050)
- **Input Length Type**: S (≤30 chars), M (31-299 chars), L (300-450 chars)
- **Input**: Singlish text to be tested
- **Expected Output**: Correct Sinhala translation
- **Actual Output**: System's actual translation (filled by automation)
- **Status**: PASS/FAIL result (filled by automation)
- **Singlish Input Types Covered**: Categories identified
- **Evidence/Rationale**: Explanation for categorization

## Results Analysis

### Automated Analysis
After running the tests, use the analysis script to categorize input types:

```bash
python fill_analysis_columns.py
```

This script will:
- Analyze each test case input
- Identify applicable Singlish input types
- Generate rationales for categorization
- Fill the analysis columns in the Excel file

### Expected Results
All 50 test cases are designed to **FAIL**, demonstrating scenarios where the transliteration system produces incorrect outputs. Common failure patterns include:

- Incorrect transliteration of English technical terms
- Mishandling of proper nouns (names, places)
- Poor handling of mixed language content
- Incorrect processing of punctuation and special characters
- Failure to preserve English abbreviations and acronyms

## Troubleshooting

### Common Issues

#### 1. Browser Not Found
```
Error: Executable doesn't exist at <path>
```
**Solution**: Install Playwright browsers
```bash
playwright install
```

#### 2. Permission Denied (Excel file)
```
PermissionError: [Errno 13] Permission denied
```
**Solution**: Close the Excel file before running tests

#### 3. Website Loading Issues
```
Error loading frontend: TimeoutError
```
**Solution**: Check internet connection and try increasing timeout:
```bash
python test_automation.py --timeout-ms 120000 [other options]
```

#### 4. Slow Performance
**Solution**: Use headless mode and reduce delays:
```bash
python test_automation.py --headless --wait-ms 2000 --type-delay-ms 30 [other options]
```

### Debug Mode
For troubleshooting, run with debug options:
```bash
python test_automation.py --keep-open --slow-mo-ms 1000 --wait-ms 8000 [other options]
```

## File Descriptions

### Core Files
- **`test_automation.py`**: Main automation script using Playwright
- **`Assignment 1 - Test cases.xlsx`**: Excel file containing all test cases and results
- **`README.md`**: This documentation file

### Utility Scripts
- **`generate_failing_test_cases.py`**: Generates the 50 unique test cases
- **`fill_analysis_columns.py`**: Analyzes and categorizes input types

## Technical Details

### Dependencies
```
playwright>=1.40.0
openpyxl>=3.1.0
```

### Browser Support
- **Primary**: Chromium (via Playwright)
- **Alternative**: Google Chrome (system installation)
- **Fallback**: Firefox, Safari (with modifications)

### Performance Considerations
- **Typical runtime**: 15-25 minutes for 50 test cases
- **Factors affecting speed**: Network latency, website responsiveness, delay settings
- **Optimization**: Use headless mode and reduce wait times for faster execution

## Academic Integrity Notice

This project is designed for educational purposes as part of the IT3040 ITPM course. The test cases are:
- **Completely original** and do not copy examples from assignment appendices
- **Unique in vocabulary and structure** to avoid plagiarism detection
- **Focused on realistic scenarios** that demonstrate system limitations
- **Properly documented** with clear rationales for categorization

## Support

For technical issues or questions:
1. Check the troubleshooting section above
2. Verify all prerequisites are installed correctly
3. Ensure stable internet connection
4. Review command line options and syntax

## License

This project is created for academic purposes as part of the SLIIT IT3040 course assignment.