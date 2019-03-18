# node-network-interfaces
This is a fork of the node Wrapper by Javier Evans around [Network-Interface-Script](https://github.com/JoeKuan/Network-Interfaces-Script) written by Joe Kuan.
Allows you to read and update the contents of your ```/etc/network/interfaces``` file.
This version does not require sudo.

## Concerns
This library is obviously only usable on systems that manage their network stack using ```/etc/network/interfaces``` although you can
point the library at any file that has the same format.

Finally, it depends on access to the ```tee``` command.

## Usage
```javascript
 const NetworkInterfaces = require('node-network-interfaces');

 const interfaces = new NetworkInterfaces('/absolute/path/to/my/interfaces/file');

 // Read the config for a given interface
 interfaces.currentConfig('eth0').then((interfaceConfig) => {
 	console.log(`Interface config was: ${interfaceConfig}`);
 }).catch((readError) => {
 	console.log(`Error reading config: ${readError}`);
 });

 // Write to the config for a given interface
 interfaces.setConfig('eth0', {
 	address: '192.168.2.12',
 	netmask: '255.255.255.0',
 	gateway: '192.168.2.1'
 }).then((newConfig) => {
 	console.log(`Config for eth0 is now ${newConfig}`);
 }).catch((configUpdateError) => {
 	console.log(`Failed to write config for eth0: ${configUpdateError}`);
 })
```

For usage sample and more information, see [this blog][2].
For updating DNS entry, see [this blog][3].

[1]: http://joekuan.wordpress.com/2009/11/01/awk-scripts-for-reading-and-editing-ubuntu-etcnetworkinterfaces-file-part-12/
[2]: http://joekuan.wordpress.com/2009/11/01/awk-scripts-for-reading-and-editing-ubuntu-etcnetworkinterfaces-file-part-22/
[3]: http://joekuan.wordpress.com/2015/10/30/awk-script-for-changing-ubuntu-network-interfaces-added-dns-feature/
