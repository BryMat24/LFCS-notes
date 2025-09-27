## ACL

---

Extension on traditional Linux file permissions, allow assign fine-grained permissions to multiple users on per-file/directory basis. Define specific permission for specific users

```
sudo apt install acl
sudo setfacl --modify user:jeremy:rw file3
sudo getfacl file3
sudo setfacl --modify mask:r file3 # limit to read only

sudo setfacl --modify group:sudo:rw file3
sudo setfacl --modify user:jeremy:--- file3
sudo setfacl --remove user:jeremy file3
sudo setfacl --remove group:sudo file3

sudo setfacl --recursive -m user:jeremy:rwx dir1/
sudo setfacl --recursive --remove user:jeremy dir1/
```

file and directory attributes. Eg. APPEND_ONLY attribute (a), and IMMUTABLE attribute

```
sudo chattr +a newfile # can only append, add new data on top of our data
sudo chattr +i newfile # cannot be changed in any way, can't rename, deleted, edited. not even root
sudo lsattr newfile
sudo chattr -i newfile

man chattr # see other attributes
```
