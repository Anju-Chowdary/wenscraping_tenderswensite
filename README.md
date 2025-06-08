# Technical Assignment: CPWD Tender Scraper

**Submitted by: Pinninti Anju Chowdary**
**Email: pinnintianju2005@gmail.com**
**Phone: 8019193656**
**Date: 12-June-2024**

## 1. Objective

The goal of this assignment was to write a Python program to scrape the first 20 "New Tenders" from the CPWD e-tendering portal (`https://etender.cpwd.gov.in/`) and save the extracted data into a `tenders.csv` file with specified column names.

## 2. Package Contents

This submission is a `.zip` file containing the following:
*   `scraper.py`: The final, working Python script.
*   `tenders.csv`: The output file with the 20 scraped tenders.
*   `requirements.txt`: A list of all necessary Python libraries.
*   `README.md`: This explanatory document.

## 3. How to Execute the Program

### Step A: System Prerequisites (Crucial)

This website employs a robust security architecture that requires a client-side application. Therefore, this script **must be run on a local Windows machine**.

1.  **Operating System:** Windows 7/10/11.
2.  **eMSigner Software:** The user must first download and install the `eMSigner` component from the "Downloads" section of the CPWD website. This is a non-negotiable prerequisite set by the website's security.

### Step B: Setting up the Python Environment

1.  Open a Command Prompt (cmd).
2.  Navigate to the project folder where you unzipped these files.
3.  Install the required Python libraries using the `requirements.txt` file:
    ```bash
    pip install -r requirements.txt
    ```

### Step C: Running the Scraper

1.  While still in the project folder in your command prompt, run the script:
    ```bash
    python scraper.py
    ```
2.  A new Chrome browser window will open and perform the scraping process automatically. The script's progress will be printed in the command prompt window.

## 4. Analysis and Justification of Implementation

This section details the challenges encountered and the final, robust solution.

### 4.1. Justification: Handling Website Security (`eMSigner`)

The target website has a strong security posture that requires the `eMSigner` desktop application to be running. This prevents scraping from standard cloud environments. The `scraper.py` script is designed to run successfully on a local Windows machine where this prerequisite is met.

### 4.2. Justification: Adapting Navigation to the Live Website

The assignment's instructions specified a navigation path that differs slightly from the live website's structure. The script correctly adapts to the real user workflow to achieve the objective:
1.  Navigate to the **"Tender Information"** dropdown menu.
2.  Click the **"All Tenders"** link.
3.  Programmatically select **"New Tenders"** from the "Status" filter.
4.  Click the **"Search"** button to apply the filter.

### 4.3. Justification: Final Strategy for Reliable Data Extraction (Pagination)

Initial attempts to change the "Show entries" dropdown proved to be unreliable, as the available options on the website are dynamic and change frequently, causing the script to fail.

To build a truly robust and reliable solution, a **pagination-based strategy** was implemented. This method mimics how a real user would browse multiple pages and is much more stable.

The script's final logic is as follows:
1.  **Scrape Page 1:** After applying the search filters, the script scrapes all available tenders on the first page (typically 10).
2.  **Navigate to Page 2:** The script then programmatically locates and clicks the **"Next"** button, which is a stable and core feature of the website's table.
3.  **Wait and Scrape Page 2:** After a brief, stable wait for the second page to load, the script scrapes the tenders from this new page until a total of 20 have been collected.

This "Next Page" approach is superior because it does not depend on the unpredictable dropdown menu, guaranteeing the successful extraction of the first 20 tenders in the correct order.
