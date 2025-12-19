## Secure User Mode

```bash
Router> enable
Router# configure terminal
Router(config)# line console 0
Router(config-line)# password YOUR_PASSWORD
Router(config-line)# login
Router(config-line)# exit
```


## Secure Privileged EXEC Mode

```bash
Router> enable
Router# configure terminal
Router(config)# enable secret YOUR_SECRET_PASSWORD
Router(config)# exit
Router(config)# write memory
```


## Secure Virtual Line

```bash
Router> enable
Router# configure terminal
Router(config)# line vty 0 4
Router(config-line)# password YOUR_PASSWORD
Router(config-line)# login
Router(config-line)# exit
```

## Encrypt All Passwords

```bash
Router> enable
Router# configure terminal
Router(config)# service password-encryption
Router(config)# exit
Router(config)# write memory
```

## Configure Banner MOTD (Message of the Day)

```bash
Router> enable
Router# configure terminal
Router(config)# banner motd # YOUR_BANNER_MESSAGE_HERE #
Router(config)# exit
Router(config)# write memory



