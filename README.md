A simple Bash tool that checks URL statuses and intelligently groups them by response type. Perfect for checking lists of social media profiles, verifying links, or auditing websites.

What it does
statuschecker.sh takes a list of URLs and organizes them into clean groups:

200 (Active) – Working pages
404 (Not Found) – Dead links
3xx (Redirects) – Pages that redirect somewhere else
Other errors – Server errors, forbidden pages, etc.
Timeouts – URLs that couldn't be reached
Inactive (Soft 404s) – Pages that return 200 OK but actually show "not found" content
The last one is particularly helpful when checking social media profiles—many platforms return a successful status code even when a profile doesn't exist.

Requirements
Bash (works on Linux, macOS, or WSL on Windows)
curl (usually pre-installed)
Basic Unix tools (grep, awk)
Most systems already have everything you need. To check if curl is installed:

Bash

curl --version
If it's missing, install it:

Ubuntu/Debian:

Bash

sudo apt update && sudo apt install curl
macOS:

Bash

brew install curl
Windows (WSL):

Bash

sudo apt update && sudo apt install curl
Installation
1. Clone the repository:

Bash

git clone https://github.com/s0deq/StatusChecker.git
cd StatusChecker
2. Make the script executable:

Bash

chmod +x statuschecker.sh
3. You're ready to go!

How to use
Basic usage
Bash

./statuschecker.sh urls.txt
This reads URLs from urls.txt and saves grouped results to Result.txt.

Custom output file
Bash

./statuschecker.sh urls.txt my-results.txt
Print to console only (no file)
Bash

./statuschecker.sh urls.txt -
Filter specific groups
Want to see only active links and 404s?

Bash

./statuschecker.sh --filter 200,404 urls.txt
Filter options:

200 – Active pages
404 – Not found
3xx – Redirects
500 – Server errors (or any other status code)
timeout – Connection failures
inactive – Soft 404s
Show help
Bash

./statuschecker.sh --help
Input file format
Create a text file with one URL per line:

urls.txt:

text

https://twitter.com/elonmusk
https://twitter.com/thisuserdoesnotexist123
https://github.com/torvalds
https://example.com/dead-link
No commas, no quotes—just plain URLs.

Example output
text

=== Active (200) ===
https://github.com/torvalds

=== Not Found (404) ===
https://example.com/dead-link

=== Inactive (Soft 404) ===
https://twitter.com/thisuserdoesnotexist123

=== Timeouts ===
https://unreachable-site.example
Understanding Soft 404s
Some websites (especially social platforms) return 200 OK even when content doesn't exist. They show a "user not found" page instead of a proper 404 error.

StatusChecker detects these by looking for common "not found" phrases in the HTML response. This helps you identify truly active profiles versus fake positives.

Troubleshooting
"Permission denied" error:

Bash

chmod +x statuschecker.sh
All URLs showing as timeout:

Check your internet connection
Disable VPN/proxy temporarily
Some URLs might be blocking automated requests
Soft 404 detection seems off:

The script uses pattern matching—some sites may need custom tuning
Feel free to open an issue with examples!
Complete command reference
Bash

./statuschecker.sh [OPTIONS] <input_file> [output_file]
Options:

Flag	Description
-h, --help	Show help message
--version	Show version
-f, --filter CODES	Show only specific groups (comma-separated)
Examples:

Bash

# Basic check
./statuschecker.sh links.txt

# Custom output
./statuschecker.sh links.txt results.txt

# Only show working links
./statuschecker.sh --filter 200 links.txt

# Show errors and timeouts
./statuschecker.sh --filter 404,timeout,500 links.txt

# Print to console
./statuschecker.sh links.txt -
Contributing
Found a bug? Have an idea? Contributions are welcome!

Areas where you can help:

Improving soft 404 detection patterns
Adding parallel processing for faster checks
Better error handling
Supporting more platforms
Just fork the repo, make your changes, and submit a pull request.

License
(Add your license here—e.g., MIT License. Create a LICENSE file in your repo if you haven't already.)

Questions?
Open an issue on GitHub and I'll help you out!
