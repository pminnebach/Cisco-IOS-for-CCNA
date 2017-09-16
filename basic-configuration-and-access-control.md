# Basic configuration and security

## The device

These are the absolute basic commands for configuring and securing the device.

This one is self-explanatory, change the hostname of the device into something you can remember and is unique in your network.

```
(config)#hostname Schelde
```

This defines a default domain-name to complete unqualified host names. To use it, you must also configure a valid DNS server

```
(config)#ip domain-name <domain name>        # eg: cisco.com
(config)#ip name-server <ip address>         # eg: 8.8.8.8
```

Disable the DNS lookup of hostname. You'll see why this is necessary if you mistype commands a lot. :D

```
(config)#no ip domain lookup
```

Set a Message Of The Day that will be displayed upon login.

```
(config)#banner motd #<message> ... <message>#
```

## Console, Aux, SSH, ...

Next we can/must configure and protect the various interfaces through which we want to configure the device. Console and aux are physical interfaces on the device, where console is the default and most know serial interface.

To configure console or aux, enter the following command.

```
(config)#line console 0
 and/or
(config)#line aux 0
```

Now the terminal changes to `(config-line)#`. This is the same for every interface, so make sure you are configuring the correct interface.

Set a password that must be entered when configuring the device via said interface. This must be set for every interface individually and can be the same, or different for every interface.

```
(config-line)#password <password>
```

```
(config-line)#login
```

Set this so that messages from the device do not pop up inline when typing commands.

```
(config-line)#logging synchronous
```

```
(config-line)#history size 15
(config-line)#exec-timeout 6 45         # 6 minutes 45 seconds
```

#### SSH

To enable SSH we must issue some additional commands.

First we must set a password used for logging in via SSH. And then we must set that passwords are encrypted in the config file.

```
(config)#enable secret <password>
(config)#service password-encryption
```

Then we must generate an RSA keypair.

```
(config)#crypto key generate rsa
```

Set the SSH version to only allow version 2.

```
(config)#ip ssh version 2
```

Set a username and password for SSH login. Optionally set `priv 15` so you only need to enter your password once when logging in and not a second time when going into privileged mode.

```
(config)#username <name> secret <password> [priv 15]
```

Now configure vty 0 to 4 \(or higher\). This means that we are configuring 4 vty's at the same time, and we can have 4 simultaneously users logged in via SSH.

```
(config)#line vty 0 4
(config-line)#transport input ssh
(config-line)#logging synchronous
```

Set login local so the local username and password db will be used for authenticating.

```
(config-line)#login local
```



