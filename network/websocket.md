# 网络：WebSocket，服务器能主动推消息的长连接

HTTP 是"问一次答一次"，聊天、实时行情这种服务器要主动推的场景，
每次轮询太浪费，WebSocket 建一次连接、双向一直通。

## 握手过程

- 客户端先发一个普通 HTTP 请求，带 `Upgrade: websocket` 头。
- 服务器回 `101 Switching Protocols`，协议就从 HTTP 切换成 WebSocket，
  之后双方都能随时发消息，不用等对方先问。

## 浏览器里最小用法

```js
const ws = new WebSocket("wss://example.com/chat");
ws.onopen = () => ws.send("hello");
ws.onmessage = (e) => console.log("收到：", e.data);
ws.onclose = () => console.log("连接断了");
```

## 实践要点

- 一定用 `wss://`（TLS 加密），`ws://` 明文会被中间网络干扰。
- 断线重连、鉴权、心跳都要自己做：常见做法是每 30 秒发一个 ping，
  一段时间内没收到 pong 就重连。
- 代理和网关要支持 Upgrade，不然握手会被拦在 101 之前。
