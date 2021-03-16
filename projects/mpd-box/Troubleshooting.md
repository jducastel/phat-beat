# Troubleshooting

## Disable PiVumeter

If you tried the VLC radio project before, you may have to [get rid of pivumter](https://forums.pimoroni.com/t/getting-rid-of-pivumeter/6187/2) like this :

> Try editing /etc/asound.conf and changing:
```
pcm.softvol_and_pivumeter {
        type softvol
        slave.pcm "pivumeter"
        control {
                name "PCM"
                card 0
        }
}
```
> to:
```
pcm.softvol_and_pivumeter {
        type softvol
        slave.pcm "hw:0,0"
        control {
                name "PCM"
                card 0
        }
}
```

Removing `/etc/asound.conf` entirely will disable the `alsamixer` command, which may be used to set global sound level.
