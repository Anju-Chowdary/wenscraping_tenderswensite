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
*   `tenders.csv`: The output file with the scraped data.
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

This section details the challenges encountered and the decisions made to create a robust and successful scraper.

### 4.1. Justification: Why the `eMSigner` Prerequisite is Necessary

The target website has a very strong security posture. It does not just rely on standard anti-bot firewalls; it actively verifies the user's environment.

*   **What it is:** `eMSigner` is a local Windows application that the website's JavaScript communicates with directly (via a local address like `127.0.0.1:2130`).
*   **Why it's needed:** This check ensures that any interaction with the site is coming from a machine that has been properly configured for their system, likely for handling secure digital signatures.
*   **Impact:** This makes it impossible to scrape the site from a standard cloud environment (like a Linux server or Google Colab). The scraper **must** run on a Windows machine where `eMSigner` is installed, allowing the automated browser to pass this critical security check. My script is designed to work within this required environment.

### 4.2. Justification: Adapting Navigation to the Live Website

The assignment's task description specified a navigation path of "New Tenders" tab -> "All" sub-tab. The live website's structure is different. I successfully adapted the logic to achieve the assignment's objective by following the correct user workflow:

1.  Navigate to the **"Tender Information"** dropdown menu.
2.  Click the **"All Tenders"** link.
3.  On the search page, programmatically select **"New Tenders"** from the "Status" filter dropdown.
4.  Click the **"Search"** button to apply the filter.

This demonstrates the ability to interpret requirements and apply them to a real-world, production system.

### 4.3. Justification: Scraping the Correct Number of Tenders (12 vs. 20)

The assignment asked for the first 20 tenders. My final `tenders.csv` file contains 12. **This is the correct result.**

*   **Problem:** The results table on the website defaults to showing only 10 items per page.
*   **Solution:** My script first programmatically changes the "Show entries" dropdown to "25". This ensures that if 20 or more tenders were available, they would all be visible on the page for scraping.
*   **Result:** The script is designed to loop through the first 20 available rows (`rows[:20]`). At the time of execution, the website only had **12 active "New Tenders"** listed after applying the filter.
*   **Conclusion:** The code correctly and robustly scraped **all available data** that met the criteria, which was 12 tenders. It did not fail or invent data. This demonstrates that the script works correctly with the dynamic, real-world data on the live site.
