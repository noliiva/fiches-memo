## Linux commands to remind

##### Edit redirections file
```
sudo nano /etc/hosts
```
##### Start a service on boot
```
sudo systemctl enable "service_name"
```
##### Install a downloaded package and its dependencies
```
sudo dpkg -i "package_name.deb"
sudo apt-get -f install
```
##### Check if a package is available
```
apt-cache search "package_name"
```
##### Search a file
```
find "my_dir" -name 'my_file.ext'
```

---
## Nano useful shortcut
| Shortcut   | Description 
|------------|-------------
| Ctrl+Alt+6 | Select
| Alt+6      | Copy
| Ctrl+K     | Cut
| Ctrl+U     | Paste
| Ctrl+O     | Save
| Ctrl+X     | Exit
