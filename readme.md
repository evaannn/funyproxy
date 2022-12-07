# funyproxy 
used in [prolapsr (aka dongforce)](https://github.com/evaannn/dongforce).


## Usage
```typescript

import { ProxyManager, ProxyServer } from 'funyproxy';


const manager = new ProxyManager();

const proxyList = [
    new ProxyServer(),
    new ProxyServer()
];

// start the proxies
for (let i = 1; i <= proxyList.length; i++) {
    const proxy = proxyList[i - 1];

    proxy.listen(8080 + i, () => {
        console.log(`Proxy server ${i} listening on port ${8080 + i}`);
    });
}

// add the proxies to the manager
for (let i = 0; i < proxyList.length; i++) {
    manager.addProxy('0.0.0.0', 8080 + i);
}

// start the manager
manager.listen(8080, () => {
    console.log('Proxy manager listening on port 8080');
});


// stop the proxies
for (let i = 0; i < proxyList.length; i++) {
    proxyList[i].close(() => {
        console.log(`Proxy server ${i} closed`);
    });
}
```


