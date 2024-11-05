# Linux Production Shell Scripts
## 1. File Backup Script

```sh
#!/bin/bash
backup_dir="/root/production_scripts"
source_dir="/root"

# Check if source directory exists
if [ ! -d "$source_dir" ]; then
  echo "Source directory $source_dir does not exist. Exiting."
  exit 1
fi

# Create the backup directory if it doesn't exist
mkdir -p "$backup_dir"

# Create a timestamped backup of the source directory
tar -czf "$backup_dir/backup_$(date +%Y%m%d_%H%M%S).tar.gz" -C "$source_dir" .

# Check if the tar command succeeded
if [ $? -eq 0 ]; then
  echo "Backup created successfully at $backup_dir."
else
  echo "Failed to create backup."
fi
```

## 2. System Monitoring Script
```sh
#!/bin/bash
threshold=90

# Monitor CPU usage and trigger alert if threshold exceeded
cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}' | cut -d. -f1)
if [ "$cpu_usage" -gt "$threshold" ]; then
echo "High CPU usage detected: $cpu_usage%"

# Add alert/notification logic here
fi
```

## 3. User Account Management Script
```sh
#!/bin/bash
username="newuser"

# Check if user exists; if not, create new user
if id "$username" &>/dev/null; then
echo "User $username already exists."
else
useradd -m "$username"
echo "User $username created."
fi
```

## 4. Log Analyzer Script
```sh
#!/bin/bash
logfile="/path/to/logfile.log"

# Extract lines with "ERROR" from the log file
grep "ERROR" "$logfile" > error_log.txt
echo "Error log created."
```

## 5. Password Generator Script
```sh
#!/bin/bash
length=12

# Generate a random password
password=$(openssl rand -base64 $length)
echo "Generated password: $password"
```

## 6. File Encryption/Decryption Script
```sh
#!/bin/bash
file="/root/production_scripts/encryption.enc"

# Check if the file exists
if [ ! -f "$file" ]; then
  echo "File $file does not exist. Exiting."
  exit 1
fi

# Encrypt the file using AES-256-CBC
openssl enc -aes-256-cbc -salt -in "$file" -out "$file.enc" -pass pass:$(openssl rand -hex 16)
echo "File encrypted: $file.enc"
```

## 7. Automated Software Installation Script
```sh
#!/bin/bash
packages=("package1" "package2" "package3")

# Install listed packages using apt-get or yum
for package in "${packages[@]}"; do
sudo yum install "$package" -y
done
echo "Packages installed successfully."
```

## 8. Network Connectivity Checker Script
```sh
#!/bin/bash
host="example.com"

# Check network connectivity by pinging a host
if ping -c 1 "$host" &>/dev/null; then
echo "Network is up."
else
echo "Network is down."
fi
```

## 9. Website Uptime Checker Script
```sh
#!/bin/bash
website="https://example.com"

# Check if website is accessible
if curl --output /dev/null --silent --head --fail "$website"; then
echo "Website is up."
else
echo "Website is down."
fi
```

## 10. Data Cleanup Script
```sh




