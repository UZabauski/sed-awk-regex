# sed-awk-regex
## sed
My configuration files are full of old values which were commented out. It's time to clean up junk yard. Use sed to.
- Clean up all comment types all the conf files in the default configuration folder.
- Don't just sed it out, for the first run just create drift files.
- If you see the drift was successful - sed the files, but preserve backups.
<details>
  <summary>My solution</summary>
  
```sh
$ mkdir -p backups | find . -type f \( -iname "*.*" ! -iname "*.bak" \) -exec sed -i'backups/*.bak' '/^#/d' {} \;
```
</details>

## awk  
I have number of ethernet interfaces. I can see their MAC addresses, but they are displayed in a wrong format. Using awk and whatever else you need, write a script, which will:
- Capture all the MAC addresses.
- Produce a capitalized, no-split one-liner for each of the addresses, like:
  - i.  Eth0 MAC: ABCDE
  - ii. Eth2 MAC: EDBCA
<details>
  <summary>My solution</summary>
  
```sh
$ ip link | awk -F ' ' '{print $2}' | paste -d " " - - | grep -v lo: | awk -F ' ' '{print toupper(substr($1,1,1)) substr($1,2) " "$2}' | awk '{print NR ".", $0}' | awk -F ' ' '{gsub(/\:/," MAC:",$2);print $1" "$2" "$3}'
```
</details>

## regex
We are sitting in front of you, a herd of nubs. We never seen regexp before. You have to explain basics to us.
<details>
  <summary>My solution</summary>
  
https://www.computerhope.com/jargon/r/regex.htm
</details>
