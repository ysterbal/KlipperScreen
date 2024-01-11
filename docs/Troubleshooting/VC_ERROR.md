# Cannot open virtual Console

If you see this line in the [log](../Troubleshooting.md):
!!! abstract "Log"
    ```sh
    xf86OpenConsole: Cannot open virtual console 2 (Permission denied)
    ```

* Run `cat /etc/X11/Xwrapper.config`

This should have the line `allowed_users=anybody` in it

* Run `cat /etc/group | grep tty`

If your username is not listed under that line, you need to add it with the following command:

```sh
usermod -a -G tty pi
```
(if your username is not 'pi' change 'pi' to your username)

Restart KlipperScreen:
```sh
sudo service KlipperScreen restart
```

If it's still failing:

add `needs_root_rights=yes` to `/etc/X11/Xwrapper.config`:

```sh
sudo bash -c "echo needs_root_rights=yes>>/etc/X11/Xwrapper.config"
```

Restart KlipperScreen:
```sh
sudo service KlipperScreen restart
```


If it's still failing try the following:

Ensure legacy X11 config file support is installed (Raspbian):
```sh
dpkg --get-selections | grep xserver-xorg-legacy
```
Should return the below if installed else nothing
```
> xserver-xorg-legacy                             install
```

Install using:
```sh
sudo apt install xserver-xorg-legacy
```

Restart KlipperScreen:
```sh
sudo service KlipperScreen restart
```


