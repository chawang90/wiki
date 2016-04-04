# SSL

## iOS Simulator SSL Proxy

1. Download and install https://www.charlesproxy.com
2. Open Charles
3. Select menu: Proxy -> SSL Proxying Settings... and add Host localhost.ssl and Port 3000
4. Select menu: Help -> SSL Proxying -> Install Charles Root Certificate in iOS Simulators

## iOS Hardware Device SSL Proxy

1. Go to Settings -> Wi-Fi -> Network Name (i) -> HTTP Proxy -> Manual
2. Enter the Server IP address of your development machine and Port 8888
3. In iOS Safari go to http://charlesproxy.com/getssl and install the root certificate

## Understanding the `jossl` command.

This section of the process can be automated with the `jossl` shell command. It is still necessary to manually set up the SSL proxy in the simulator and on the device.

Create a private key (enter temporary passphrase):
```
$ openssl genrsa -des3 -out server.orig.key 2048
```

Remove the passphrase:
```
$ openssl rsa -in server.orig.key -out server.key
```

Generate the CSR:
```
$ openssl req -new -key server.key -out server.csr
```

Be sure to set the Common Name to `localhost.ssl` (browsers expect a `.` char in the domain name):
```
...
Common Name: localhost.ssl
...
```

Generate the self-signed certificate:
```
$ openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
```

Place the `key` and `crt` file in `~/.josephine/`

Add localhost.ssl to your hosts file:
```
$ echo "127.0.0.1 localhost.ssl" |sudo tee -a /private/etc/hosts
```

Add `server.key` to keychain:
1. Open Keychain Access
2. Drag `server.crt` to System Keychain
3. Open `localhost.ssl`
4. Open Trust
5. Set "When using this certificate:" to "Always Trust"

Add `server.crt` to iOS Simulator:
1. Load the Simulator
2. Drag `server.crt` into the window
3. Click "Install"

Boot thin:
```
$ thin start --ssl --ssl-key-file ~/.josephine/server.key --ssl-cert-file ~/.josephine/server.crt
```
