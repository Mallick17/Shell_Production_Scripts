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
#!/bin/bash
directory="/root"

# Remove files older than 10 days in specified directory
find "$directory" -type f -mtime +10 -exec rm {} \;
echo "Old files removed."
```

## 11. CPU Usage Tracker Script
```sh
#!/bin/bash
output_file="cpu_usage_log.txt"

# Log current CPU usage to a file with timestamp
cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}')
echo "$(date) CPU usage: ${cpu_usage}%" >> "$output_file"

echo "CPU usage logged."
```

## 12. System Information Script
```sh
#!/bin/bash
output_file="system_info.txt"

# Gather system information and save to a file
echo "System Information:" > "$output_file"
echo "-------------------" >> "$output_file"
echo "Hostname: $(hostname)" >> "$output_file"
echo "OS: $(uname -a)" >> "$output_file"
echo "Memory: $(free -h)" >> "$output_file"
echo "Disk Space: $(df -h)" >> "$output_file"
echo "System info saved to $output_file."
```

## 13. Task Scheduler Script
```sh
#!/bin/bash
scheduled_task="/root/system_information.sh"
schedule_time="0 2 * * *"
# Schedule a task using cron
echo "$schedule_time $scheduled_task" | crontab -
echo "Task scheduled successfully."
```

## 14. Disk Space Monitoring Script
```sh
#!/bin/bash
threshold=90

# Monitor disk usage and trigger alert if threshold exceeded
disk_usage=$(df -h | grep "/dev/sda1" | awk '{print $5}' | cut -d'%' -f1)

# Check if disk_usage is empty or not a number
if [[ -z "$disk_usage" || ! "$disk_usage" =~ ^[0-9]+$ ]]; then
  echo "Failed to retrieve disk usage or no disk usage data found."
  exit 1
fi

if [ "$disk_usage" -gt "$threshold" ]; then
  echo "High disk usage detected: $disk_usage%"
  # Add alert/notification logic here
fi
```

## 15. Remote Server Backup Script(Not Executed)
```sh
#!/bin/bash

# Define source directory and remote server details
source_dir="/path/to/source"
remote_server="user@remoteserver:/path/to/backup"

# Check if source directory exists
if [ ! -d "$source_dir" ]; then
    echo "Source directory does not exist: $source_dir"
    exit 1
fi

# Run rsync command to backup files to the remote server
rsync -avz --progress "$source_dir" "$remote_server"

# Check if rsync was successful
if [ $? -eq 0 ]; then
    echo "Files successfully backed up to remote server."
else
    echo "An error occurred during the backup."
    exit 1
fi
```

## 16. Environment Setup Script(Not Upto the Mark)
```sh
#!/bin/bash
# Customize for your specific environment setup
echo "Setting up development environment..."

# Install necessary packages, configure settings, etc.
echo "Development environment set up successfully."
```

## 17.  File Compression/Decompression Script()
```sh
#!/bin/bash
file_to_compress="/path/to/file.txt"

# Compress a file using gzip
gzip "$file_to_compress"
echo "File compressed: $file_to_compress.gz"
```

## 18. Database Backup Script()
```sh
#!/bin/bash
database_name="your_database"
output_file="database_backup_$(date +%Y%m%d).sql"

# Perform database backup using mysqldump
mysqldump -u username -ppassword "$database_name" > "$output_file"
echo "Database backup created: $output_file"
```

## 19. Git Repository Updater Script
```sh
#!/bin/bash
git_repo="/path/to/your/repo"

# Update a Git repository
cd "$git_repo"
git pull origin master
echo "Git repository updated."
```

## 20. Directory Synchronization Script()
```sh
#!/bin/bash
source_dir="/path/to/source"
destination_dir="/path/to/destination"

# Synchronize directories using rsync
rsync -avz "$source_dir" "$destination_dir"
echo "Directories synchronized successfully."
```

## 21.  Web Server Log Analyzer Script()
```sh
#!/bin/bash
log_file="/var/log/apache2/access.log"

# Analyze web server log to count unique IP addresses
awk '{print $1}' "$log_file" | sort | uniq -c | sort -nr
echo "Web server log analyzed."
```

## 22. System Health Check Script
```sh
#!/bin/bash
output_file="system_health_check.txt"

# Perform system health check and save results to a file
echo "System Health Check:" > "$output_file"
echo "---------------------" >> "$output_file"
echo "Uptime: $(uptime)" >> "$output_file"
echo "Load Average: $(cat /proc/loadavg)" >> "$output_file"
echo "Memory Usage: $(free -m)" >> "$output_file"
echo "System health check results saved to $output_file."
```

## 23. Automated Database Cleanup Script()
```sh
#!/bin/bash
database_name="your_database"
days_to_keep=7

# Clean up old database backups older than specified days
find /path/to/database/backups -name "$database_name*.sql" -mtime
+"$days_to_keep" -exec rm {} \;
echo "Old database backups cleaned up."
```

## 24. User Password Expiry Checker Script()
```sh
#!/bin/bash
# Check password expiry for users with bash shell
IFS=$'\n'
for user in $(cat /etc/passwd | grep "/bin/bash" | cut -d: -f1); do
password_expires=$(chage -l "$user" | grep "Password expires" |
awk '{print $4}')
echo "User: $user, Password Expires: $password_expires"
done
unset IFS
```

## 25.  Service Restart Script
```sh
#!/bin/bash
service_name="your_service"

# Restart a specified service
sudo systemctl restart "$service_name"
echo "Service $service_name restarted."
```

## 26.  Folder Size Checker Script
```sh
#!/bin/bash
folder_path="/path/to/folder"

# Check and display the size of a specified folder
du -sh "$folder_path"
echo "Folder size checked."
```

## 27. Backup Rotation Script()
```sh
#!/bin/bash
backup_dir="/path/to/backups"
max_backups=5

# Rotate backups by deleting the oldest if more than max_backups
while [ $(ls -1 "$backup_dir" | wc -l) -gt "$max_backups" ]; do
oldest_backup=$(ls -1t "$backup_dir" | tail -n 1)
rm -r "$backup_dir/$oldest_backup"
done
echo "Backup rotation completed."
```

## 28. Remote Script Execution Script()
```sh
#!/bin/bash
remote_server="user@remote-server"
remote_script="/path/to/remote/script.sh"

# Execute a script on a remote server via SSH
ssh "$remote_server" "bash -s" < "$remote_script"
echo "Remote script executed."
```sh
```

## 29. Network Interface Information Script()
```sh
#!/bin/bash
network_interface="eth0"

# Display network interface information
ifconfig "$network_interface"
echo "Network interface information displayed."
```

## 30. Random Quotes Generator Script
```sh
#!/bin/bash
quotes=("Quote 1" "Quote 2" "Quote 3" "Quote 4")

# Generate and display a random quote from the array
random_index=$((RANDOM % ${#quotes[@]}))
echo "Random Quote: ${quotes[$random_index]}"
```


