# 📄 Case Study: End-to-End Crash Analysis & Reporting Automation

### 📊 Executive Summary

This is a case study of a comprehensive, two-part automation solution I designed and deployed at Synamedia to address the time-consuming and manual process of daily crash analysis. The solution utilized **Playwright** for data extraction and triage and **Power BI** for automated reporting, completely eliminating a 2-3 hour daily manual task and providing the team with automated, interactive crash data insights.

---

### ⚠️ The Challenge: Manual & Inefficient Crash Triage

The existing process for handling daily kernel and panic crashes from `BugSplat` was entirely manual, requiring 2-3 hours of an engineer's time each day. The workflow involved:
* Manually downloading dozens of crash reports.
* Running separate, manual shell scripts to process different crash types.
* Visually inspecting backtraces to identify the crash type, component, and uniqueness.
* Manually compiling all findings into an Excel sheet.
* Manually creating new `Jira` tickets or updating existing ones with comments.

This process was not only slow ⏳ but also highly susceptible to human error.

---

### ✨ My Solution: A Two-Part Automated System

I engineered a robust, unattended system that runs automatically every morning at 9 AM.

#### Part 1: Automated Crash Triage & Analysis 🤖 (Playwright & Shell Scripting)

I developed a core script using `Playwright` that orchestrates the entire triage process:
1.  **Automated Data Extraction:** The script logs into `BugSplat`, automatically filters for the correct date and product version, downloads all crash files, and organizes them into a structured folder system (`crashes/type/version/environment`).
2.  **Intelligent Kernel Crash Processing:** For kernel crashes, the script parses each backtrace and compares it against a historical database in Excel. If a new backtrace has more than three non-matching lines compared to existing records, it is classified as a new crash.
3.  **Automated Panic Crash Processing:** For panic crashes, the script automates the entire shell workflow. It connects to the dev server, converts `.dmp` files to `.core` files, moves them to a box server, and processes them to generate the final backtrace.
4.  **Jira Integration & Reporting:** The system automatically generates two key text files:
    * `jira.txt`: A daily summary of all crashes, their component, the corresponding Jira ticket link, and the device MAC ID.
    * `backtrace.txt`: A clean list of all new backtraces that need to be updated in `Jira`, significantly speeding up the debugging process.

#### Part 2: Automated & Interactive Reporting 📈 (Power BI)

To provide the team with high-level insights, I automated the reporting pipeline:
1.  **Centralized Data Source:** The daily crash reports are automatically saved to a shared `OneDrive` folder.
2.  **Dynamic Dashboard:** I built a `Power BI` dashboard connected to this folder. It provides interactive visualizations and allows any team member to filter crash data by type, component, date, and version.
3.  **Automated Delivery:** The `Power BI` report is scheduled to automatically refresh and email a summary to all team members every Monday morning, ensuring consistent stakeholder visibility.

---

### 🏆 Key Achievements & Quantifiable Impact

* **100% Unattended Automation:** The entire process runs automatically at 9 AM daily with zero human intervention. 🤖
* **Time Savings:** **Eliminated 2-3 hours of manual work per day**, freeing up valuable engineering time. ⏰
* **Error Reduction:** Removed the risk of human error in data entry and backtrace analysis. ✅
* **Enhanced Insights:** The `Power BI` dashboard empowered the team with self-service, interactive data exploration, leading to faster identification of crash trends. 💡
* **Improved Communication:** Automated weekly email reports ensured all stakeholders were consistently informed of stability metrics. 📧

---

### 💻 Technologies Used

* **Automation:** Playwright, Python, Shell Scripting
* **Business Intelligence:** Microsoft Power BI, Power Query
* **Data Management:** Microsoft Excel, OneDrive
* **DevOps Tools:** Jira, BugSplat
