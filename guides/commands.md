# Born2beRoot Commands

## SSH

Start OpenSSH

```sh
$ sudo /etc/init.d/ssh start
$ sudo service ssh start
$ sudo systemctl start ssh
```

Stop OpenSSH

```sh
$ sudo /etc/init.d/ssh stop
$ sudo service ssh stop
$ sudo systemctl stop ssh
```

Restart OpenSSH

```sh
$ sudo /etc/init.d/ssh restart
$ sudo service ssh restart
$ sudo systemctl restart ssh
```

Status of OpenSSH

```sh
$ sudo /etc/init.d/ssh status
$ sudo service ssh status
$ sudo systemctl status ssh
```

Enable and start OpenSSh at boot time

```sh
$ sudo systemctl enable ssh
```

Check if OpenSSH is enabled at boot time

```sh
$ sudo systemctl is-enabled ssh
```

## UFW

Display UFW rules

```
$ sudo ufw status numbered
$ sudo ufw status
```

Enable UFW

```
$ sudo ufw enable
$ sudo systemctl enable ufw
```

Disable UFW

```
$ sudo ufw disable
```

Add UFW rule

```
$ sudo ufw allow <port number>
```

Delete UFW rule

```
$ sudo ufw delete <rule number>
$ sudo ufw delete allow <port number>
```
