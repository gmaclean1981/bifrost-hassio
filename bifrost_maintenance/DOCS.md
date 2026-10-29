# Configuration, migration and rollback

## Configuration

Create `/config/bifrost/config.yaml` in Home Assistant's shared configuration
directory (for example through Samba). Replace every example value below with
your network details. The bridge IP/MAC must refer to the Home Assistant host's
interface on the network serving Hue clients. Zigbee2MQTT must expose its
WebSocket backend and be reachable from Bifrost.

```yaml
bridge:
  name: Bifrost
  mac: 02:00:00:00:00:01
  ipaddress: 192.0.2.10
  netmask: 255.255.255.0
  gateway: 192.0.2.1
  timezone: Etc/UTC
z2m:
  server1:
    url: ws://192.0.2.20:8080
```

The addresses above are documentation examples. Authentication and other options
are described in the [source configuration reference](https://github.com/gmaclean1981/bifrost/blob/master/doc/config-reference.md).
The app uses host networking and the existing upstream NET_ADMIN/AppArmor settings;
it has write access to the shared configuration directory for Bifrost's state.
HTTP/HTTPS and discovery ports must be available, with appropriate reachability
between Hue clients, Home Assistant and Zigbee2MQTT.

## Moving from a local or upstream app

1. Stop the old Bifrost app and turn its **Start on boot** off.
2. Back up the complete shared `/config/bifrost` directory, including configuration,
   certificate and state. Keep the backup private: it may include credentials.
3. Install this app without uninstalling the old app. The repository installation
   has its own app ID even if its short slug resembles an existing local app.
4. Keep the shared directory intact so the existing bridge identity is preserved.
5. Start only this app. Check logs, your existing Hue app connection and a light.
6. Enable **Start on boot** on this app once validated. Leave it off on old apps.

## Rollback

1. Stop this app and disable its **Start on boot** setting.
2. Preserve a separate copy of its current `/config/bifrost` directory.
3. Restore the complete stopped-state backup from before the switch, if returning
   to the previous saved state. This reverses Bifrost changes made since then.
4. Start the retained old app and verify Hue controls. Enable Start on boot only
   for the build you choose to keep running.

Never run two Bifrost apps against the same state or ports simultaneously.
