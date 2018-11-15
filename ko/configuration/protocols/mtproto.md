---
refcn: chapter_02/protocols/mtproto
refen: configuration/protocols/mtproto
---
# MTProto

* 이름 : `mtproto`
* 유형 : 인바운드 / 아웃 바운드

MTProto 프록시는 전보를위한 특별한 프로그램입니다. V2Ray의 인바운드 프록시와 아웃 바운드 프록시로 구성됩니다. 그들은 보통 전보를위한 프록시를 만들기 위해 함께 사용됩니다

현재 V2Ray는 텔레 그램 서버의 IPv4 주소 만 지원합니다.

## InboundConfigurationObject

```javascript
{
  "users": [{
    "email": "love@v2ray.com",
    "level": 0,
    "secret": "b0cbcef5a486d9636472ac27f8e11a9d"
  }]
}
```

> `명의 사용자`: \ [[UserObject](#userobject)\]

사용자 배열. 현재로서는 첫 번째 사용자 만 효과적입니다.

### UserObject

```javascript
{
  "email": "love@v2ray.com",
  "level": 0,
  "secret": "b0cbcef5a486d9636472ac27f8e11a9d"
}
```

> `이메일`: 문자열

사용자 이메일. 추적 목적으로 사용됩니다. [통계보기](../stats.md).

> `레벨`: 숫자

사용자 수준.

> `비밀`: 문자열

사용자 비밀. 텔레 그램에서 사용자 비밀은 32 자이어야하며 `0` 에서 `9`사이의 문자와 `a`에서 `f`사이의 문자 만 포함해야합니다.

{% hint style='tip' %}

You may use the following command to generate MTProto secret: `openssl rand -hex 16`

{% endhint %}

## 아웃 바운드 구성 {#outbound}

```javascript
{
}
```

## 견본 {#sample}

MTProto can only be used for Telegram traffic. You may need a routing rule to combine the corresponding inbound and outbound. Here is an incomplete sample.

Inbound:

```javascript
{
  "tag": "tg-in",
  "port": 443,
  "protocol": "mtproto",
  "settings": {
    "users": [{"secret": "b0cbcef5a486d9636472ac27f8e11a9d"}]
  }
}
```

Outbound:

```javascript
{
  "tag": "tg-out",
  "protocol": "mtproto",
  "settings": {}
}
```

Routing:

```javascript
{
  "type": "field",
  "inboundTag": ["tg-in"],
  "outboundTag": "tg-out"
}
```

The configure your Telegram app to connect to 443 port on this machine.