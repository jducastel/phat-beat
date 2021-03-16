# Manual installation

## MPD / MPC installation / configuration

Install MPD (server/daemon) and MPC (client)
```shell
apt-get install mpd mpc
```

`mpc` client won't be able to retrieve / adjust volume until editing configuration file at `/etc/mpd.conf` to replace line

```
audio_output {
  mixer_type "hardware"
}
```

by

```
audio_output {
  mixer_type "software"
}
```
