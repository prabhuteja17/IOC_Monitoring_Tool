# IOC_Monitoring_Tool
A Python based tool for monitoring IOCs, reanalyzing threat intelligence in VirusTotal, and sending automated alerts via Outlook 
IOC Tracking and Email Notification System

# 📌 Overview
This project automates the tracking of Indicators of Compromise (IOCs) by:

✅ Reanalyzing IOCs in VirusTotal before fetching updated threat scores
✅ Checking FireEye & McAfee detections (for SHA256 IOCs)
✅ Updating an Excel sheet with the latest IOC scores
✅ Sending email notifications for IOCs that exceed a malicious threshold

# ⚙️ Features
✅ Reads IOC data from an Excel file
✅ Reanalyzes IOCs in VirusTotal before fetching their score
✅ Handles rate limits and retries when needed
✅ Extracts FireEye & McAfee detection results for SHA256 IOCs
✅ Prompts user before removing malicious IOCs from tracking
✅ Sends an email notification with flagged IOCs
✅ Attaches an Excel file with the malicious IOCs

# 🛠️ Installation
    1️⃣ Clone the Repository
    git clone https://github.com/your-repo/ioc-tracking.git  
    cd ioc-tracking  
    2️⃣ Install Dependencies
    Ensure Python 3.8+ is installed, then run:
    pip install pandas openpyxl requests pywin32  
    3️⃣ Configure API Keys
    Replace the placeholder with your VirusTotal API keys in the script:
    VIRUSTOTAL_API_KEYS = ["your_api_key_1", "your_api_key_2"]
    
# 🚀 Usage
  1️⃣ Prepare the Input Excel File
      Ensure ioc_tracking.xlsx contains the following columns:
      DateName of AnalystMalware NameIOCIOC ValueCurrent ScoreStatus
      The script updates the "Current Score" based on VirusTotal results.
      If an IOC exceeds the malicious threshold (5), it is flagged for review.
      
  2️⃣ Run the Script
      python ioc_tracker.py  
      
  3️⃣ User Prompt for Malicious IOCs
      Yes → Removes malicious IOCs from tracking.
      No → Updates their status to "Malicious".
      
  4️⃣ Email Notification
  Sends an Outlook email with:
      A table of flagged IOCs
      An attached Excel file listing malicious IOCs
      Formatted in Times New Roman (Size 10)
      
# 🔍 How It Works
  Step 1: Read IOC Data
  Loads ioc_tracking.xlsx into a Pandas DataFrame
  Iterates through each IOC
  
  Step 2: Reanalyze IOC in VirusTotal
  Calls VirusTotal API to request reanalysis
  Waits up to 100 seconds for the latest results
  
  Step 3: Fetch Updated Score
  Gets the latest malicious score from VirusTotal
  Extracts FireEye & McAfee detection results for SHA256 IOCs
  
  Step 4: Determine Malicious IOCs
  If score ≥ 5, the IOC is flagged
  If SHA256 is detected by FireEye & McAfee, it is excluded from blocking
  
  Step 5: Prompt User for Removal
  If Yes, remove malicious IOCs from Excel
  If No, update their status to "Malicious"
  
  Step 6: Send Email Notification
  Includes flagged IOCs in a formatted table
  
# Attaches an Excel report
Uses Outlook to send the email

# 🔄 API Response Handling
Reanalysis & Score Fetching

Reanalysis Request: POST /analyse

Fetching Latest Score: GET /domains/{ioc}

Error Handling:
Error CodeHandling Strategy404IOC not found → Set score to 0429Rate limit exceeded → Wait 30 seconds and retry500API failure → Skip IOC and log error

# 📂 Code Structure
ioc-tracking/

│── ioc_tracker.py   # Main script

│── utils.py         # Helper functions (API handling, email formatting)

│── ioc_tracking.xlsx # Input Excel file

│── README.md        # Documentation

# 📈 Future Improvements
🔹 Enhance reanalysis polling (reduce wait time)
🔹 Add logging mechanism for error tracking
🔹 Support alternative email providers (SMTP-based)

# 🤝 Contributing
Fork the repository
Create a feature branch (git checkout -b feature-new)
Commit your changes (git commit -m "Added new feature")
Push to the branch (git push origin feature-new)

# Open a Pull Request
📜 License
This project is private and meant for internal cybersecurity use.

# 📧 Contact
👤 SABHAVAT PRABHU TEJA 📧 Contact: prabhusabhavat@gmail.com
