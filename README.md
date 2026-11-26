# Automated Process Logger Scheduling System

Python automation script that periodically scans a directory, detects duplicate files by MD5 checksum, deletes duplicate copies, creates a timestamped log file, and sends the log by email.

The script keeps the first copy found for each checksum and removes the remaining copies.

## Features

- Recursively scans a directory and its subdirectories
- Groups identical files using MD5 checksums
- Deletes duplicate copies while keeping one original
- Creates timestamped `.log` reports in the `Marvellous` directory
- Sends the report as an email attachment through Gmail SMTP
- Runs repeatedly at a configurable interval using `schedule`
- Provides command-line help options

## Project Structure

```text
Automated-Process-Logger-Scheduling-System-/
|-- DuplicateFileRemoval.py
|-- DuplicateFiles/
|-- Marvellous/
|-- requirements.txt
|-- README.md
`-- .gitignore
```

## Requirements

- Python 3
- Windows PowerShell or Command Prompt
- Internet access
- A Gmail account configured to send the report

Install the project dependencies:

```powershell
cd "e:\Github_Repos\Automated-Process-Logger-Scheduling-System-"
python -m pip install -r requirements.txt
```

## Run the Script

Open PowerShell in the project directory and use:

```powershell
python DuplicateFileRemoval.py "<AbsoluteDirectoryPath>" <IntervalInMinutes> "<ReceiverEmailAddress>"
```

Example:

```powershell
python DuplicateFileRemoval.py "e:\Github_Repos\Automated-Process-Logger-Scheduling-System-\DuplicateFiles" 10 "receiver@example.com"
```

The script:

1. Checks that the provided path is a directory.
2. Waits for the configured interval before running its first scheduled scan.
3. Compares files using MD5 checksums.
4. Removes duplicate copies.
5. Writes a report to `Marvellous\DuplicateRemovalLog_<timestamp>.log`.
6. Emails the report as an attachment.
7. Continues running until stopped.

Stop the running script with `Ctrl+C`.

## Command-Line Help

Display detailed help:

```powershell
python DuplicateFileRemoval.py --h
```

Display usage information:

```powershell
python DuplicateFileRemoval.py --u
```

The usage requires all three arguments:

```text
python DuplicateFileRemoval.py <AbsoluteDirectoryPath> <TimeIntervalInMinutes> <ReceiverEmailAddress>
```

## Example Scanned Log

The script creates reports such as:

```text
Marvellous/DuplicateRemovalLog_<dd_mm_yyyy_HH_MM_SS>.log
```

A report includes:

- Directory scan start and completion times
- Scanned directory path
- Number of unique file groups scanned
- Duplicate file paths
- MD5 checksum values
- Number of duplicate files deleted

## Safety Notice

This script deletes files permanently. It does not move duplicates to a recycle bin or backup folder.

Test it with a copy of a directory before running it on important data. The script keeps the first file encountered and deletes the other files with the same checksum.

## Email Configuration

The script currently uses Gmail SMTP on port `465` and contains the sender credentials in `DuplicateFileRemoval.py`.

For a real deployment:

1. Remove hardcoded credentials from the source code.
2. Create and use a Gmail App Password.
3. Store the sender address and App Password in environment variables or a secure configuration file.
4. Update `Send_mail()` and `smtp.login()` to read those credentials securely.

Never commit real passwords or App Passwords to a Git repository.
