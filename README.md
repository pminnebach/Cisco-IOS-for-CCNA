# Cisco IOS

These are my notes on how to configure Cisco IOS routers and switches through the CLI via serial or SSH.

There are different modes to operate the device, and not every command is available in every mode.

The first mode is the one we enter when we initialy connect to the device. This can be recognized by a single _angle bracket_.

```
Router>
```

Not a lot can be done in this mode, so we best get into **user mode.**

```
Router>enable
```

The angle bracket will change into a _pound sign_.

To enter **privileged mode**, we issue the following command.

```
Router#configure terminal
```

Now it shows you what you are configuring between parentheses.

```
Router(config)#
```

Depending on what you are configuring the `config` between the parentheses will change into `config-line`, `config-if`, `dhcp-config`, etc.

Also note that `Router` here is the name of the device. When we change the hostname in the next chapter, this will also change in the CLI. I will omit this in the rest of this book and only show the important part that defines which mode we are configuring.

**Quick recap**

```
Router>
Router#                # User mode
Router(config)#        # Privileged mode
```

Now we can start with the fun stuff.

