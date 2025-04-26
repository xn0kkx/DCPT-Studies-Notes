# Log File Analysis Commands

A consolidated set of pipeline commands for analyzing web server logs (e.g., `access.log`). Each example explains the purpose, the individual components, and usage.

---

## Extract Unique Client IPs

### Remove Duplicate IPs
```bash
cat access.log \
  | cut -d ' ' -f1 \
  | sort -u
```
- **`cat access.log`**: Reads the entire log file.
- **`cut -d ' ' -f1`**: Splits each line on spaces and extracts the 1st field (the client IP).
- **`sort -u`**: Sorts the IPs alphabetically and removes duplicates, yielding a list of unique IP addresses.


## Count IP Occurrences

### Show Count per IP (Ascending)
```bash
cat access.log \
  | cut -d ' ' -f1 \
  | sort \
  | uniq -c
```
- **`sort`**: Sorts IPs so `uniq` can group identical ones.
- **`uniq -c`**: Counts consecutive identical lines, prefixing each IP with its occurrence count.

### Show Count per IP (Descending)
```bash
cat access.log \
  | cut -d ' ' -f1 \
  | sort \
  | uniq -c \
  | sort -nr
```
- **`sort -nr`**: Sorts lines numerically (`-n`) and in reverse order (`-r`), listing the most active IPs first.


## Find First and Last Occurrence of an IP

### First Access Line for an IP
```bash
grep "177.138.28.7" access.log \
  | head -n 1
```
- **`grep "IP" access.log`**: Filters lines containing the given IP.
- **`head -n 1`**: Prints only the first matching line.

### Last Access Line for an IP
```bash
grep "177.138.28.7" access.log \
  | tail -n 1
```
- **`tail -n 1`**: Prints only the last matching line.


## Extract and Count Request Paths

### Extract Request URLs
```bash
grep "177.138.28.7" access.log \
  | cut -d '"' -f2
```
- **`cut -d '"' -f2`**: Splits on double quotes and extracts the 2nd field (the HTTP request verb and path, e.g., `GET /index.html HTTP/1.1`).

### Count Most Frequent Request URLs
```bash
grep "177.138.28.7" access.log \
  | cut -d '"' -f2 \
  | sort \
  | uniq -c \
  | sort -nr
```
- Identical to the IP-counting pipeline but applied to request lines.


## Filter by HTTP Status Codes

### Show Only `200` Responses for an IP
```bash
grep "177.138.28.7" access.log \
  | awk -F']' '{ print $2 }' \
  | grep " 200 "
```
- **`awk -F']' '{ print $2 }'`**: Splits each line at the first `]` (end of timestamp), printing the remainder (status code, size, referrer, etc.).
- **`grep " 200 "`**: Filters to only lines with status code `200`.


## Search for Specific Directory Access

```bash
grep "177.138.28.7" access.log \
  | grep "/restricted/"
```
- **Double `grep`**: First filter for the IP, then for any request path containing `/restricted/`.


---

# Additional Useful Log Analysis Commands

## Monitor New Log Entries in Real Time
```bash
tail -f access.log
```
Keeps the terminal open, appending new log entries as they arrive.

## Count All `404` (Not Found) Responses
```bash
grep -c " 404 " access.log
```
**`grep -c`** counts matching lines without printing them.

## List HTTP Status Codes with Counts
```bash
awk '{ print $9 }' access.log \
  | sort \
  | uniq -c \
  | sort -nr
```
- **`$9`**: In common log formats, the 9th field is the status code.

## Count Requests Per Hour
```bash
awk '{ split($4, time, ":"); print time[2] }' access.log \
  | uniq -c \
  | sort -nr
```
- **`split($4, time, ":")`**: Splits the timestamp (`[dd/Mon/yyyy:HH:MM:SS`) on `:`, extracting the hour (`time[2]`).

## Filter by Date
```bash
grep "01/Apr/2025" access.log | wc -l
```
Counts log entries for April 1, 2025.

