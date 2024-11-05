# Linux Production Shell Scripts
## 1. File Backup Script
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
