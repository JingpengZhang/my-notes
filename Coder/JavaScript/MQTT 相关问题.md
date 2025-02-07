1. `ws` 连接成功，但 `wss` 连接失败
2. 
连接 `ws://mqtt.showinfo.com.cn:8083/mqtt` 时成功，连接 `wss://mqtt.showinfo.com.cn:8084/mqtt` 时失败，在 `chrome` 浏览器下无报错信息，换到 `safari` 浏览器后报错：

```js
WebSocket connection to 'wss://mqtt.showinfo.com.cn:8084/mqtt' failed: The certificate for this server is invalid. You might be connecting to a server that is pretending to be “mqtt.showinfo.com.cn” which could put your confidential information at risk.
```
