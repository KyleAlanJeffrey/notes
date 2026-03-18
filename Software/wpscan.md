Word Press Scanner

Enumeration Options
```
-e, --enumerate [OPTS] Enumeration Process Available Choices: 
vp Vulnerable plugins 
ap All plugins 
p Popular plugins 
vt Vulnerable themes 
at All themes 
t Popular themes 
tt Timthumbs 
cb Config backups 
dbe Db exports 
u User IDs range. e.g: u1-5 Range separator to use: '-' Value if no argument supplied: 1-10 
m Media IDs range. e.g m1-15 Note: Permalink setting must be set to "Plain" for those to be detected Range separator to use: '-' Value if no argument supplied: 1-100 Separator to use between the values: ',' 
Default: All Plugins, Config Backups Value if no argument supplied: vp,vt,tt,cb,dbe,u,m Incompatible choices (only one of each group/s can be used):
```
### Common Usages

**Enumerate Users and output to file**
```
wpscan --url url --enumerate u -o file.txt
```

**Enumerate Plugins**
```
wpscan --url url --enumerate u
```
