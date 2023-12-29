# Changing uinput Device Permission

## Target: To change the /dev/uinput permission to allow non-root application to open/read/write the device file
### Creating A New Group: `uinput`

    > Add new group by following command
```bash
   sudo groupdadd -f uinput
   sudo gpasswd -a username uinput
```
    > Verify username has been added into uinput group
```bash
   groups
```

### Creating New udev Rule

    > create a new file name: `/etc/udev/rules.d/99-input.rules`
    > Insert the following in the code
```bash
   KERNEL=="uinput", MODE="0660", GROUP="uinput", OPTIONS+="static_node=uinput"
```
    > Machine reboot or run this to reload
```bash
   sudo sh -c ‘udevadm control –reload; udevadm trigger -v –name-match uinput’
```
    > Verify settings by following command:
```bash
   ls -l /dev/uinput
```
```bash
   crw-rw---- 1 root uinput 10, 223 Nov 11 15:35 /dev/uinput
```

