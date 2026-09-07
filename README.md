# Automation Log Analysis

Extends the beginner-level manual log
review by automating the scan of a Linux log file for suspicious activity — failed
logins, authentication failures, and unknown/invalid users — using a simple Python
script in VS Code. The scan is scoped to log lines 200–500 to simulate handling larger
data more efficiently.

## Prerequisites

- Beginner-level log review project completed (basic familiarity with the log format).
- [VS Code](https://code.visualstudio.com/) installed.
- Python 3.x installed and available on your PATH.
- Basic familiarity with running a Python script from a terminal.

## Project Files

| File | Description |
|------|--------------|
| `log_analysis.py` | Python script that scans the log and flags suspicious entries. |
| `Linux_2k.log` | Sample Linux log file from [LogHub](https://github.com/logpai/loghub), same file used in the beginner project. |
| `suspicious_logs.csv` | Generated output — CSV report of flagged entries (created after running the script). |

## How It Works

1. **Read the log file** — opens `Linux_2k.log` and reads all lines into a list.
2. **Focus on lines 200–500** — slices the list to `logs[199:500]` (Python is
   0-based, so index 199 is line 200) to simulate targeted analysis of a larger
   dataset.
3. **Search for suspicious patterns** — checks each line in the subset for:
   - `"Failed password"` → tagged **Failed Login**
   - `"authentication failure"` → tagged **Auth Failure**
   - `"user unknown"` or `"invalid user"` → tagged **Unknown User**
4. **Print results** — outputs every flagged entry with its tag, plus a total count.
5. **Export to CSV** — saves all flagged entries to `suspicious_logs.csv` with
   `Type` and `Log Entry` columns for easy review in Excel or Google Sheets.

## Usage

1. Make sure `log_analysis.py` and `Linux_2k.log` are in the same folder.
2. Open this folder in VS Code.
3. Open a terminal in VS Code and run:

   ```bash
   python log_analysis.py
   ```

4. Review the printed output in the terminal, and open `suspicious_logs.csv` in
   Excel/Google Sheets for a more structured view of the results.

## Example Output

```
=== Suspicious Log Entries (Lines 200-500) ===
[Auth Failure] Jun 22 03:17:26 combo sshd(pam_unix)[16206]: authentication failure; logname= uid=0 euid=0 tty=NODEVssh ruser= rhost=n219076184117.netvigator.com user=root
[Auth Failure] Jun 22 03:17:35 combo sshd(pam_unix)[16210]: authentication failure; logname= uid=0 euid=0 tty=NODEVssh ruser= rhost=n219076184117.netvigator.com user=root
...

Total suspicious entries found: <N>
Results saved to suspicious_logs.csv
```

## Skills Practiced

- Python scripting applied to a cybersecurity task.
- Extracting and analyzing a specific range of log lines.
- Automated detection of failed logins, authentication failures, and unknown users.
- Generating a CSV report — a skill directly applicable to SOC (Security Operations
  Center) workflows.

## Possible Extensions

- Parameterize the line range (200–500) instead of hardcoding it.
- Extract and count offending IP addresses/hostnames (`rhost=`) to spot repeat offenders.
- Add timestamp parsing to sort or filter entries by time of day.
- Scan the entire log file instead of a fixed subset.
