# Guide to WebRTC�� �����鼭 ������ �͵�.

��ũ : https://www.baeldung.com/webrtc

---

## ����

- [Guide to WebRTC�� �����鼭 ������ �͵�.](#guide-to-webrtc��-�����鼭-������-�͵�)
  - [����](#����)
  - [- Sending a Message](#--sending-a-message)
  - [Overview](#overview)
  - [Fundamentals anc Concepts of WebRTC](#fundamentals-anc-concepts-of-webrtc)
    - [������ Ŀ�´����̼�](#������-Ŀ�´����̼�)
  - [Support for WebRTC and Built-In Features(���� ��� ����)](#support-for-webrtc-and-built-in-features����-���-����)
  - [Peer-to-Peer Connection](#peer-to-peer-connection)
  - [Signaling](#signaling)
    - [Building the Signaling Server](#building-the-signaling-server)
    - [Creating Message Handler in Signaling Server](#creating-message-handler-in-signaling-server)
  - [Exchanging Metadata](#exchanging-metadata)
  - [Setting Up the Client](#setting-up-the-client)
  - [Setting Up a Simple RTCDataChannel](#setting-up-a-simple-rtcdatachannel)
  - [Establishing a Connection With ICE](#establishing-a-connection-with-ice)
    - [Creating an Ofter](#creating-an-ofter)
    - [Handling ICE Candidates](#handling-ice-candidates)
    - [Receiving the ICE Candidate](#receiving-the-ice-candidate)
    - [Receiving the Offer](#receiving-the-offer)
    - [Receiving the Answer](#receiving-the-answer)
  - [Sending a Message](#sending-a-message)
---

## Overview

2���� �������� Ŀ�´�����Ʈ�� �ʿ��� ��, ���� �׵� ���� �޼����� �ְ�ޱ� ���� Ŀ�´����̼��� ���� ������ ������ �ʿ��ϴ�.

�׷��� �߰��� ������ �����ϴ� ���� �������鰣 Ŀ�´����̼ǿ��� delay�� �߱��Ѵ�.

���⼭ WebRTC�� �������� ����� applications���� �ǽð����� ���� ���� Ŀ�´�����Ʈ�� �� �ְ� ���ش�.

���⿡���� HTML, JavaScript �� WebSocket ���̺귯���� �� �������� ����� WebRTC ������ �Բ� ����Ͽ� client�� ������ ���̴�.

�׸���, WebSocket�� ��� �������ݷ� ����ϴ� Spring Boot�� Signaling Server�� ���� ���̴�.

����������, �� ���ῡ ���� �� ����� ��Ʈ���� �߰��ϴ� ����� �˾ƺ����̴�.

---

## Fundamentals anc Concepts of WebRTC

### ������ Ŀ�´����̼�

WebRTC ���� 2���� ������ �� �������� Ŀ�´����̼��� ��� �ϴ��� ���� ���ڴ�.

2���� �������� �ִٰ� �����ϰ�, Browser 1�� Brower2���� �޼����� ������ ���Ҷ�, �׷��� �Ʒ��� ���� Browser1�� Server���� ���� �޼����� ������.

- ![b1](./readme_img/b1.JPG)

Server�� �޼����� ���� ��, �װ��� ó���ϰ�, Browser2�� ã��, message�� �Ʒ��� ���� ������.
- ![b2](./readme_img/b2.JPG)

�̶�, browser2���� �޼����� ������ �� Server���� �����ϱ� ������, Ŀ�´����̼��� ���� �ǽð����� �̷������. ����, ���⼭ ��¥ real-time���� �̷������ ���Ѵ�.

WebRTC�� �� ������ ���̿� ���� ä���� ����� server�� �ʿ伺�� ���������ν� �� ������ �ذ��Ѵ�.
- ![webrtc](./readme_img/webrtc.JPG)

���������, �޽����� sender���� receiver�� ���� ����õǹǷ� �� ���������� �ٸ� �������� �޽����� �����ϴ� �� �ɸ��� �ð��� ũ�� ����ȴ�.

---

## Support for WebRTC and Built-In Features(���� ��� ����)

WebRTC�� Chrome, ... �� �ƴ϶� Android, iOS �����ȴ�.

**WebRTC�� �������� �Բ� ��� �����Ǵ� solution�̱� ������ �������� �ܺ� �÷������� ��ġ ���ص� �ȴ�.**

�Դٰ�, �������� ���� ����� ������ ������ real-time application����, ���� C++ ���̺귯���� ���ϰ� �����ϸ�, �̿����� �Ʒ��� ���� ���� �������� �ִ�.
```
Packet-loss concealment
Echo cancellation
Bandwidth adaptivity
Dynamic jitter buffering
Automatic gain control
Noise reduction and suppression
Image ��cleaning��
```

**WebRTC�� �̷��� ��� ������ �ذ�**�ϹǷ� client �� �ǽð� Ŀ�´����̼��� ���� �����ϰ� ������ �� �ִ�.

---

## Peer-to-Peer Connection

P2P ���ῡ�� server�� ���� �˷��� �ּҰ� �ְ� client�� �̹� ����� server�� �ּҸ� �˰� �ִ� client-server�� �ٸ���, **�ٸ� peer�� ���� �������� �ּҸ� ���� peer�� ����.**

�� p2p ������ �����ϱ� ����, client���� ������ ����ؾ��Ѵ�.
```
1. ������ Ŀ�´����̼��� �����ϵ��� �ؾ���.
2. ���� �ĺ��� �Ǿ���ϰ� ��Ʈ��ũ ���� ������ �����ؾ���.
3. ���õ� data, mode, protocols ������ �����ϰ� �����ؾ���.
4. �����͸� �����ؾ���.
```

WebRTC�� �̷��� �ܰ���� �����ϱ� ���� API�� methodologies(�����)�� �����Ѵ�.

client�� ���� �߰��ϰ�, ��Ʈ��ũ ���� ������ ������ ����, data�� ������ �����ϱ� ���� **WebRTC�� signaling�̶�� ��Ŀ���� ���.**

---

## Signaling

Signaling�� ��Ʈ��ũ �˻�, session ����, session ����, media-��� ��Ÿ������ ��ȯ�� ���õ� processes�� ���Ѵ�.

�̰��� client���� ���ο� ���� �̸� �˾ƾ� Ŀ�´����̼��� ������ �� �ֱ⿡ �ʼ����̴�.

�̸� �̷�� ���ؼ���, **WebRTC�� signaling�� ���� ǥ���� Ư������ �ʰ� �������� ������ �ñ��.**

### Building the Signaling Server

signaling server�� ���, Spring Boot�� ����Ͽ� WebSocket server�� �����ϰڴ�. Spring Initializer���� ������ empty Spring Boot ������Ʈ�� ������ �� �ִ�.

������ WebSocket�� ����ҷ��� �Ʒ��� ���� �������踦 ������.(xml)
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-websocket</artifactId>
    <version>2.4.0</version>
</dependency>
```

signaling server ������ ������
- client application�� WebSocket ����� ����ϴ� �� ����� �� �ִ� endpoint�� �����.
- �̰��� Spring Boot���� �ϱ� ���ؼ��� �Ʒ��� ���� �ؾ���.
- @Configuration, implements WebSocketConfigurer, override registerWebSocketHandlers method
- 
```java
@Configuration
@EnableWebSocket
public class WebSocketConfiguration implements WebSocketConfigurer {

    @Override
    public void registerWebSocketHandlers(WebSocketHandlerRegistry registry) {
        registry.addHandler(new SocketHandler(), "/socket")
          .setAllowedOrigins("*");
    }
}
```

���� �ܰ迡�� ������ client���� ����� URL�� `/socket`���� �ĺ���.

����, SocketHandler�� addHandeler method�� ���� argument�� ������. - �̰� ������ ���� �޼��� ��鷯��.(�Ʒ� ����)

### Creating Message Handler in Signaling Server

���� �ܰ�� ���� clients���� ���� WebSocket �޽����� ó���ϴ� �޽��� �ڵ鷯�� �ۼ��ϴ� ���̴�.

**�̴� ���� WebRTC ������ �����ϱ� ���� �ٸ� clients�� ��Ÿ������ ��ȯ�� �����ϱ� ���� �ʼ����̴�.**

���⼭�� �ܼ��ϰ�, client�κ� �޽����� ������, �װ��� �ڽ��� ������ �ٸ� ��� clients���� ���� ���̴�.

�̰��� �ϱ����ؼ�, Spring WebSocket library�� `extend TextWebSocketHandler`�ؾ��ϰ� `handleTextMessage`�� `afterConnectionEstablished` method�� override�ؾ��Ѵ�.

```java
@Component
public class SocketHandler extends TextWebSocketHandler {

    List<WebSocketSession>sessions = new CopyOnWriteArrayList<>();

    @Override
    public void handleTextMessage(WebSocketSession session, TextMessage message)
      throws InterruptedException, IOException {
        for (WebSocketSession webSocketSession : sessions) {
            if (webSocketSession.isOpen() && !session.getId().equals(webSocketSession.getId())) {
                webSocketSession.sendMessage(message);
            }
        }
    }

    @Override
    public void afterConnectionEstablished(WebSocketSession session) throws Exception {
        sessions.add(session);
    }
}
```

`afterConnectionEstablished` method���� ������, ���� session�� session ��Ͽ� �߰��Ͽ� ��� client���� track �� �� �ִ�.

�׸��� `handleTextMessage`���� ���̴� �� ó�� cliens�κ��� �޽����� ������, �츮�� list�� ��� clients sesions�� iterate�ϰ� ��������� session ID�� list�� session�� �������ν� ��������� ������ ��� clients���� �޽����� ������.

--

## Exchanging Metadata

P2P connection����, clients�� ���� �ſ� �ٸ� �� �ִ�. �������, Android������ Chrome�� Mac������ Mozilla�� ���� �� �� �ִ°� ó��

�׷��Ƿ�, �̷��� ��ġ���� �̵�� ����� �ſ� �پ��� �� �ִ�. ����, Peer�鰣 handshake�� ��ſ� ���Ǵ� �̵�� ������ �ڵ��� �����ϴ� ���� �߿��ϴ�.

�̷��� ���鿡��, **WebRTC�� clients�� metadat agree�� SDP(Session Description Protocol)�� ����Ѵ�.**

�̸� �̷�� ����, initiating peer�� �ٸ� peer�� ���� descriptor�� �ݵ�� �����ؾ� �ϴ� offer�� �����.

���Ͽ�, �ٸ� peer�� initiating peer�� ���� ���� descriptor�� ���Ǵ� answer�� �����Ѵ�.

�� ó���� �Ϸ�ɶ� connection�� �����ȴ�.

---

## Setting Up the Client

initiating peer�� ���� peer�� ������ ��� ������ �� �ֵ��� WebRTC client�� �����.

`index.html`�̶�� �Ҹ��� HTML filee�� `index.html`�� ����� `client.js`��� �Ҹ��� JavaScript file�� ���������ν� �����Ѵ�.

signaling server�� �����ϱ� ���ؼ�, WebSocket ������ �����. 

�츮�� ������ Spring Boot signaling server�� local���� ����ȴٰ� �����ϸ� �Ʒ��� ���� ������ ���� �� �ִ�.
```javascript
var conn = new WebSocket('ws://localhost:8080/socket');
```

signaling server�� message�� ������ ���ؼ�, ���� �ܰ迡�� �޽����� �����ϱ� ���� send method�� ������̴�.
```javascript
function send(message){
    conn.send(JSON.stringify(message));
}
```

---

## Setting Up a Simple RTCDataChannel

`client.js`���� client�� setting ��, **RTCPeerConnection** class�� ���� object ������ �ʿ��ϴ�.
```javascript
configuratoin = null;
var peerConnection = new RTCPeerConnection(configuratoin);
```

�� ����������, configuration object�� ������ STUN(Session Traversal Utilities for NAT)�� TURN(Traversal Using Relays around NAT) servers �� �� Ʃ�丮���� �Ĺݺο��� ������ �ٸ� configurations�� �����ϴ� ���̴�.

�� ������ ��� null�� �����ϸ� �����.

�޽��� �н̿� ����� `dataChannel`�� ������ �� �ִ�.

�� �Ŀ�, data channel�� �پ��� �̺�Ʈ�� ���� listeners�� ������ �� �ִ�.

---

## Establishing a Connection With ICE

WebRTC connection�� �����ϴ� �����ܰ�� ICE(Interactive Connection Establishment) �� SDP protocols�� ���ԵǸ�, ���⼭ peers�� session description�� �� peers���� ��ȯ �� ����(accept)�ȴ�.


signaling server�� peers �� ������ ������ �� ���ȴ�. ���⿡�� clients�� signaling server�� ���� connection metadat�� ��ȯ�ϴ� �Ϸ��� �ܰ谡 ���Եȴ�.

### Creating an Ofter

ù��°��, offer�� �����ϰ� �̸� `peerConnection`�� local description���� �����Ѵ�. �׷� ���� �ٸ� peer���� offer�� ������.
```javascript
peerConnection.createOffer(function (offer){
    send({
        event : "offer",
        data : offer
    });
    peerConnection.setLocalDescription(offer);
},function(error){
    //Handle error here
});
```

���⿡, send method�� signaling server�� offer ������ �����ϱ� ���� call �ؾ��Ѵ�.

### Handling ICE Candidates

�ι�°, ICE candidates handle�� �ʿ��ϴ�.

**WebRTC�� connection�� �����ϰ� peers�� �߰��ϴ� ICE(Interactive Connection Establishment) protocol�� ����Ѵ�.**

`peerConnection`���� local description�� �����Ҷ�, `icecandidate` event�� Ʈ�����Ѵ�.

�� event�� ���� peer�� �ش� ���� peer�� �߰��� �� �ֵ��� �ش� candidate�� ���� peer�� �����ؾ��Ѵ�.

�̰��� �ϱ�����, `onicecandidate` event�� ���� listener�� �������Ѵ�.
```javascript
peerConnection.onicecandidate = function (event){
    if(event.candidate){
        send({
            event : "candidate",
            data : event.candidate
            });
    }
};
```

`icecandidate` event�� ��� candidates�� ���̸� empty candidate string���� �ٽ� Ʈ���ŵȴ�.

�� cnadidate object�� ���� peer���� �����ؾ� �Ѵ�.

�� empty candidate string�� �����Ͽ� ���� peer�� ��� icecandidate objects�� �𿴴ٴ°��� �� �� �ֵ��� �ؾ��Ѵ�.

����, ������ event�� �ٽ� Ʈ���ŵǾ� ICE �ĺ� ������ event���� candidate object�� ���� null�� ���������� ��Ÿ����. �̰��� ���� peer�� ������ �ʿ䰡 ����,

### Receiving the ICE Candidate

����°, �ٸ� peer�� ���� ICE CANDIDATE�� ó���ؾ� �Ѵ�.

���� PEER�� �� candidate�� ���� �� �ش� candidate pool�� �߰��ؾ��Ѵ�.
```javscript
peerConnection.addIceCandidate(new RTCIceCandidate(candidate));
```


### Receiving the Offer

�� ��, �ٸ� peer�� offer�� �޾��� ��, remote description�� �����ؾ� �Ѵ�. ���� initiating peer�� ���۵Ǵ� answer(����)�� �����ؾ� �Ѵ�.

```javascript
peerConnection.setRemoteDescription(new RTCSessionDescription(offer));
peerConnection.createAnswer(function(answer) {
    peerConnection.setLocalDescription(answer);
        send({
            event : "answer",
            data : answer
        });
}, function(error) {
    // Handle error here
});
```

### Receiving the Answer

����������, **initiating peer�� answer�� �ް� ���� description���� �����Ѵ�.**
```javascript
handleAnswer(answer){
    peerConnection.setRemoteDescription(new RTCSessionDescription(answer));
}
```

�̷����ϸ�, WebRTC�� �������� ������ ����ȴ�.

���ݺ���, **signaling server���� �� peers�� ���� data�� �ְ���� �� �ִ�,**

---

## Sending a Message

�츮�� connection�� �����߰�, **`dataChannel`�� send method�� ����Ͽ� peers �� �޽������� ���� �� �ִ�.**

```javascript
dataChannel.sned("message");
```

����������, �ٸ� peer�� message�� �ޱ� ���ؼ���, `onmessage` event listener�� �������Ѵ�.
```javascript
dataChannel.onmessage = function(event){
  console.log("Message:",event.data);
};
```

data channel���� message�� �ޱ� ���ؼ���, �츮�� ���� `peerConnection` object�� callbalk�� �߰��ؾ��Ѵ�.
```javascript
peerConnection.ondatechannel = function(event){
  dataChannel = event.channel;
};
```

�̷��� ��������, �츮�� ������ functional WebRTC data channel�� �������. ������ clients�� data�� �ְ� �ް� �� �� �ִ�. �߰�������, �츮�� ���⿡ ������ ����� channel�� �߰��� �� �ִ�.

---

Adding Video 