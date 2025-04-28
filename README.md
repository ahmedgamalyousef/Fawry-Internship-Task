# 🔲 Fawry Internship Task 

## ❓ Quiz 1 : Custom Command (`mygrep.sh`)

### 🧠 Reflective Section

#### 1. How does your script handle arguments and options?

##### 🎯 **Argument :**
- The script checks if there are at least two remaining arguments after processing the options:
  - **`search_word`**: The text to search for .
  - **`filename`**: The file to search in .

##### ⚙️ **Option :**
- Each option starting with `-` is processed using `getopts`:
  - **`-v`**: Inverts the match (prints lines that do not contain the search string).
  - **`-n`**: Shows the line number before the matching text .
  
- The script allows options to be written in different formats :
  - **Together**: `-vn` .
  - **Separate**: `-v -n` .
  - **In any order**: `-v -n` or `-n -v` .

##### 🔄 **How Options Work Together :**
- If the user uses `-vn` or `-nv`, both options (`-n` and `-v`) will be activated, regardless of the order .

#### 2. Supporting Regex or Additional Options (`-i`, `-c`, `-l`) :

- To add features like regex, **`-i`** (case-insensitive), **`-c`** (count matches), and **`-l`** (list file names with matches), the script needs some changes :
  - **Regex Support**: Use `grep -E` to support regular expressions and allow pattern-based searches .
  - **`-i`** (Case-Insensitive) : Modify the script to handle case-insensitive searches by adding `-i` in `grep` .
  - **`-c`** (Count Matches): Instead of showing matching lines, print the total number of matches .
  - **`-l`** (List File Names): Show only file names that have matches, not the matching lines .

#### 3. 🏆 Most Hard Part of Script Implementation :

- The hardest part of the script was handling combined options (like `-vn` and `-nv`) and making sure the script processes them correctly. Options can be written together or separately, so it was important to ensure the script handles them the same way regardless of the order .

##### ❓ **Why was this part hard ?**
- Users might mix up the order or combine options in unexpected ways .
- It was essential to ensure the script handles these cases without errors or surprises .

##### 🛠️ **How was this handled?**
- `getopts` was used to process the options, ensuring consistent behavior whether options are combined or separate .
- The script also checks for missing search strings and filenames and provides clear error messages when needed .

#### 4.✨ **Bonus Features**
- Added support for `--help`  flag to print usage instructions .
- Improved command-line option parsing using getopts for cleaner and more efficient handling of`-n` and `-v`options .

#### 5. 📷 Screenshots
- All Results is saved in Folder called `Screenshots/Quiz1` .

## ❓ Quiz 2 : Scenario 
### 🛠️ Internal Service DNS/Network Troubleshooting Report
###### 📋 Scenario
- The internal service `internal.example.com` is unreachable .
- Users are seeing “host not found” errors .
- Task is to troubleshoot, verify, and restore access .
##### 1. Verify DNS Resolution
##### Commands Used :
```bash
dig internal.example.com
dig @8.8.8.8 internal.example.com
curl -v http://internal.example.com
telnet internal.example.com
sudo netstat -tuln | grep '80\|443'
cat /etc/hosts
cat /etc/resolv.conf
nslookup internal.example.com
nslookup internal.example.com 8.8.8.8
ping internal.example.com

```
- We found that the server can't be reached using DNS or 8.8.8.8 , then start to apply temporary solution
##### 🔧 Temporary Solution:
- Added a manual entry to /etc/hosts file :
```
192.168.43.139      internal.example.com
```
- After modification, the /etc/hosts file looks like :
```
192.168.43.139 internal.example.com
127.0.0.1 localhost
127.0.0.1 minio
127.0.0.1 www.jemy.com
127.0.1.1 Ahmed-Gamal
192.168.100.1 node1 node1.jemy.com
192.168.100.2 node2 node2.jemy.com
#The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```
#### 2. Test Local DNS Resolution
##### 🖱️ Command:
```
ping internal.example.com
```
##### ⏳ Output :
```
PING internal.example.com (192.168.43.139) 56(84) bytes of data.
64 bytes from internal.example.com (192.168.43.139): icmp_seq=1 ttl=64 time=0.095 ms
64 bytes from internal.example.com (192.168.43.139): icmp_seq=2 ttl=64 time=0.028 ms
64 bytes from internal.example.com (192.168.43.139): icmp_seq=3 ttl=64 time=0.063 ms
64 bytes from internal.example.com (192.168.43.139): icmp_seq=4 ttl=64 time=0.076 ms
64 bytes from internal.example.com (192.168.43.139): icmp_seq=5 ttl=64 time=0.074 ms
64 bytes from internal.example.com (192.168.43.139): icmp_seq=6 ttl=64 time=0.067 ms
64 bytes from internal.example.com (192.168.43.139): icmp_seq=7 ttl=64 time=0.054 ms
64 bytes from internal.example.com (192.168.43.139): icmp_seq=8 ttl=64 time=0.075 ms
64 bytes from internal.example.com (192.168.43.139): icmp_seq=9 ttl=64 time=0.043 ms
64 bytes from internal.example.com (192.168.43.139): icmp_seq=10 ttl=64 time=0.089 ms
64 bytes from internal.example.com (192.168.43.139): icmp_seq=11 ttl=64 time=0.073 ms
64 bytes from internal.example.com (192.168.43.139): icmp_seq=12 ttl=64 time=0.069 ms
64 bytes from internal.example.com (192.168.43.139): icmp_seq=13 ttl=64 time=0.025 ms
64 bytes from internal.example.com (192.168.43.139): icmp_seq=14 ttl=64 time=0.074 ms

```
#### 3. Test Web Service on Port 80
##### 💻 Command:
```
sudo python3 -m http.server 80
```
##### 📡 Output:
```
Serving HTTP on :: port 80 (http://[::]:80/) ...
```
#### 4. Test HTTP Response via curl
##### 🌐 Command:
```
curl http://internal.example.com
```
##### 💥 Output:
```
<html>
<head><title>502 Bad Gateway</title></head>
<body>
<center><h1>502 Bad Gateway</h1></center>
<hr><center>nginx/1.24.0 (Ubuntu)</center>
</body>
</html>
```
#### 5. 📷 Screenshots
- All Results is saved in Folder called `Screenshots/Quiz2` .