# Fix A2DP for Teams Linux

This was originally posted at [StackExchange](https://askubuntu.com/questions/1085480/bluetooth-headphones-switches-from-a2dp-sink-to-hsp-hfp-when-starting-voip-a/1119934#1119934?newreg=d4b00929a92541afaf3400051f8fd5e0).

> From pulseaudio 10.0 release notes:
> Pulse release notes wrote: Bluetooth headsets typically support both the A2DP profile, which is suitable for music, and the HSP profile, which is suitable for telephony use cases. module-bluetooth-policy will now automatically switch the profile of a Bluetooth headset from A2DP to HSP/HFP when an application creates a recording stream with property media.role=phone (telephony applications should set that property for their streams). When the stream goes away, the profile gets restored back to A2DP. This way the user doesn't have to manually switch the profiles when starting and stopping a call. This behaviour can be disabled by giving argument auto_switch=false to module-bluetooth-policy.

Basically you need to change this line in the file `/etc/pulse/default.pa`:

```
### Automatically load driver modules for Bluetooth hardware
ifexists module-bluetooth-policy.so
load-module module-bluetooth-policy
.endif
```

To:

```
### Automatically load driver modules for Bluetooth hardware
ifexists module-bluetooth-policy.so
load-module module-bluetooth-policy auto_switch=false
.endif
```

# Fix cedilha

Para teclados internacionais, o cedilha não aparece corretamente. Para consertar, basta editar o arquivo `~/.local/share/applications/teams.desktop` e adicionar:

```
env GTK_IM_MODULE=cedilla teams %U
```
