#!/bin/bash

# Usage: ./query_logger.sh <database_name> <sql_file> <log_file>

# Validate input arguments
if [ "$#" -ne 3 ]; then
    echo "Usage: $0 <database_name> <sql_file> <log_file>"
    exit 1
fi

# Assign arguments to variables
DATABASE_NAME=$1
SQL_FILE=$2
LOG_FILE=$3

# Check if the SQL file exists
if [ ! -f "$SQL_FILE" ]; then
    echo "Error: SQL file '$SQL_FILE' does not exist."
    exit 1
fi

# Create or clear the log file
> "$LOG_FILE"

# Log the start time
echo "Query Execution Log" >> "$LOG_FILE"
echo "-------------------" >> "$LOG_FILE"
echo "Execution started at: $(date)" >> "$LOG_FILE"
echo >> "$LOG_FILE"

# Execute the query and append the result to the log file
echo "Running query from '$SQL_FILE' on database '$DATABASE_NAME'..." >> "$LOG_FILE"

if mysql -u username -p password "$DATABASE_NAME" < "$SQL_FILE" >> "$LOG_FILE" 2>&1; then
    echo "Query executed successfully." >> "$LOG_FILE"
else
    echo "Error occurred while executing the query." >> "$LOG_FILE"
fi

# Log the end time
echo >> "$LOG_FILE"
echo "Execution ended at: $(date)" >> "$LOG_FILE"

# Notify the user
echo "Query execution log saved to '$LOG_FILE'."
every year old 