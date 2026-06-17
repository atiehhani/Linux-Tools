## 1- Copy ALL directories (not files) from /root/lotus to the docs repo
This command copies only the directory structure, not the files inside them:  
```bash
cd /root/lotus && find . -type d -not -path "./.git*" -not -path "." | while read dir; do mkdir -p "/tmp/docs_repo/${dir#./}"; done
```
## 2- If you want to copy directories WITH their files and subdirectories:
```bash
cp -r /root/lotus/* /tmp/docs_repo/ 2>/dev/null || true
```
### Or, if you want to copy only specific directories (e.g., only those that start with certain names):  
Example: Copy only directories starting with "project_"  
```bash
cd /root/lotus && for dir in project_*/; do [ -d "$dir" ] && cp -r "$dir" /tmp/docs_repo/; done
```
## 3- Copy all directories except the deepest level
```bash
cd /root/lotus && find . -type d -not -path "./.git*" -not -path "." | while read dir; do 
    # Check if this directory has any subdirectories
    if [ -z "$(find "$dir" -mindepth 1 -maxdepth 1 -type d 2>/dev/null)" ]; then
        # This is a leaf directory (no subdirectories), skip it
        echo "Skipping leaf directory: $dir"
    else
        # This directory has subdirectories, create it
        mkdir -p "/root/docs_repo/${dir#./}"
        echo "Created: $dir"
    fi
done
```
## 4- Exclude directories at a specific depth  
For example, to create only directories up to level 2 (meaning level 3 and deeper are skipped):  
```bash
# Copy only directories up to 2 levels deep (skip level 3 and beyond)
cd /root/lotus && find . -type d -not -path "./.git*" -not -path "." | while read dir; do
    depth=$(echo "$dir" | tr -cd '/' | wc -c)
    if [ $depth -lt 3 ]; then
        mkdir -p "/root/docs_repo/${dir#./}"
        echo "Created: $dir"
    else
        echo "Skipping (depth > 2): $dir"
    fi
done
```
### To skip only the deepest level (whatever depth), use this simpler approach:   
```bash
cd /root/lotus && find . -type d -not -path "./.git*" -not -path "." | while read dir; do
    # Check if directory contains any other directories
    if [ $(find "$dir" -maxdepth 1 -type d | wc -l) -gt 1 ]; then
        # Has subdirectories, so create it
        mkdir -p "/root/docs_repo/${dir#./}"
        echo "Created: $dir"
    else
        echo "Skipping (no subdirectories): $dir"
    fi
done
```
## 5- Copy only parent directories (skip all leaf nodes)
```bash
cd /root/lotus && find . -type d -not -path "./.git*" -not -path "." | while read dir; do
    # Check if this directory has child directories
    has_children=$(find "$dir" -mindepth 1 -maxdepth 1 -type d 2>/dev/null | wc -l)
    if [ $has_children -gt 0 ]; then
        mkdir -p "/root/docs_repo/${dir#./}"
        echo "Created parent directory: $dir"
    else
        echo "Skipping leaf directory: $dir"
    fi
done
```
## 6- Skip directories at maximum depth
This finds the maximum depth first, then skips directories at that depth:  
```bash
cd /root/lotus
max_depth=$(find . -type d -not -path "./.git*" -not -path "." | tr -cd '/' | wc -c | sort -nr | head -1)

find . -type d -not -path "./.git*" -not -path "." | while read dir; do
    depth=$(echo "$dir" | tr -cd '/' | wc -c)
    if [ $depth -lt $max_depth ]; then
        mkdir -p "/root/docs_repo/${dir#./}"
        echo "Created: $dir (depth: $depth)"
    else
        echo "Skipping deepest level: $dir (depth: $depth)"
    fi
done
```
### Simple one-liner to skip deepest level
```bash
cd /root/lotus && find . -type d -not -path "./.git*" -not -path "." -exec sh -c '[ $(find "$1" -maxdepth 1 -type d | wc -l) -gt 1 ] && mkdir -p "/root/docs_repo/${1#./}"' _ {} \;
```
