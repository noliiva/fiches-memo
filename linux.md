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

##### ENOSPC bug fix
```
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```

#### Remove git .ori
```
find . -name "*.orig" -type f -delete
```

#### Update a node module localy
```
cd ~/my_dir/my_library_dir && yarn build && cd ~/my_dir/my_project && rm -rf node_modules/my_library/es && rm -rf node_modules/my_library/lib && cp -R ~/my_dir/my_library/es node_modules/my_library && cp -R ~/my_dir/my_library_dir/lib node_modules/my_library && yarn build:dll
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
