---
title: DKDK Open API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - php
  - javascript
  - python

toc_footers:
  - <div class="fb-like" data-href="https://www.facebook.com/dkdkheart" data-width="100" data-layout="button_count" data-action="like" data-size="small" data-show-faces="false" data-share="false"></div>
  - <a href='http://dkdk.io/dev/'>DKDK 개발자홈</a>
  - <a href='http://facebook.com/dkdkheart'>DKDK 페이스북</a>
  - <a href='http://dkdk.io/'>DKDK 홈</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>
  - © 2019 <a href='http://aply.biz'>APLY Inc.</a>
includes:
  - errors

search: true
---

# 소개

'오늘도 어제처럼 두근두근'

두근두근 Open API의 사용 설명서입니다

# Token 발급 받기

> Open API 의 사용을 위해 DKDK 개발자 Token을 발급 받으세요.


```shell

```

```php

```

```javascript

```

```python

```


>

DKDK Open API는 DKDK 개발자 Token을 파라메터로 입력해야 사용하실 수 있습니다.
아래 경로에서 먼저 개발자Token을 발급 받으세요.

[DKDK 개발자Token 발급](http://dev.dkdk.io/dev/register/index.html).

발급받은 Token의 사용방법은 각 Open API의 설명을 참고해 주세요.

<aside class="notice">
DKDK Open API를 사용하시려면 반드시 <code>Token</code>을 API의 파라메터로 입력해야 합니다. 간수에 유의해 주세요.
</aside>

# 친구 요청/수락/헤어지기

## 친구 요청하기

```shell

curl -H "dkdk-token: DKDKTOKEN" -H "Content-type: application/json" -X POST -d '{"action":"request", "user_uuid" : "MY_UUID", "friend_nickname" : "FRIEND_NICKNAME"}' http://api.dkdk.io/v1/dkdk

```

```php

$body['action'] = 'request';
$body['user_uuid'] = 'MY_UUID';
$body['friend_nickname'] = "FRIEND_NICKNAME";

$headers = array(
        'Content-Type: application/json',
        'dkdk-token: DKDKTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.dkdk.io/v1/dkdk');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "request", "user_uuid" : "MY_UUID", "friend_nickname" : "FRIEND_NICKNAME"};

$.ajax({url : "https://api.dkdk.io/v1/dkdk",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("dkdk-token", "DKDKTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           alert("Successfully, recorded.");
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'dkdk-token' : 'DKDKTOKEN'
}
data = {
    'action': 'request',
    'user_uuid' : 'USER_UUID'
    'friend_nickname' : "FRIEND_NICKNAME"
}
url = 'https://api.dkdk.io/v1/dkdk'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 API는 친구요청에 성공했을 경우 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result": "success",
    "friend_uuid": "FRIEND_UUID"
  }
```

친구요청을 전송합니다.

### HTTP 요청

`POST http://apis.dkdk.io/v1/dkdk`

### URL 파라메터

파라메터 | 설명
--------- | -----------
dkdk-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
user_uuid | 개발자 등록시 부여받은 user_uuid를 입력합니다.
action | 'request'를 입력합니다.
friend_nickname | 친구요청을 전송할 대상의 닉네임을 입력합니다.

<aside class="warning">
Token의 노출에 유의하세요!
</aside>

## 친구요청 수락하기


```shell

curl -H "dkdk-token: DKDKTOKEN" -H "Content-type: application/json" -X POST -d '{"user_uuid":"USER_UUID", "action":"accept", "friend_uuid" : "FRIEND_UUID"}' http://api.dkdk.io/v1/dkdk

```

```php

$body['action'] = 'accept';
$body['user_uuid'] = 'USER_UUID';
$body['friend_uuid'] = 'FRIEND_UUID';

$headers = array(
        'Content-Type: application/json',
        'dkdk-token: DKDKTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.dkdk.io/v1/dkdk');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;

```

```javascript


var jdata = {"action": "accept", "user_uuid" : "USER_UUID", "friend_uuid" : "FRIEND_UUID" };

$.ajax({url : "https://api.dkdk.io/v1/dkdk",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("dkdk-token", "DKDKTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'dkdk-token' : 'DKDKTOKEN'
}
data = {
    'action': 'accept',
    'user_uuid' : 'USER_UUID'
    'friend_uuid' : 'FRIEND_UUID'
}
url = 'https://api.dkdk.io/v1/dkdk'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()


```
> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
{
  "result" : "success"
}

```

친구요청을 수락합니다.

### HTTP 요청

`POST http://api.dkdk.io/v1/dkdk`

### URL 파라메터

파라메터 | 설명
--------- | -----------
dkdk-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
action | 'accept'을 입력합니다.
user_uuid | 개발자 등록시 부여받은 user_uuid를 입력합니다.
friend_uuid | 친구요청 전송에 성공했을때 수신한 friend_uuid를 입력합니다.

## 친구와 헤어지기

```shell

curl -H "dkdk-token: DKDKTOKEN" -H "Content-type: application/json" -X POST -d '{"user_uuid":"USER_UUID", "action":"bye", "friend_uuid" : "FRIEND_UUID"' http://api.dkdk.io/v1/dkdk

```

```php

$body['action'] = 'bye';
$body['user_uuid'] = 'USER_UUID';
$body['friend_uuid'] = "FRIEND_UUID";

$headers = array(
        'Content-Type: application/json',
        'dkdk-token: DKDKTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.dkdk.io/v1/dkdk');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "bye", "user_uuid" : "USER_UUID", "friend_uuid" : "FRIEND_UUID"};

$.ajax({url : "https://api.dkdk.io/v1/dkdk",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("dkdk-token", "DKDKTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'dkdk-token' : 'DKDKTOKEN'
}
data = {
    'action': 'bye',
    'user_uuid' : 'USER_UUID'
    "friend_uuid" : "FRIEND_UUID"
}

url = 'https://api.dkdk.io/v1/dkdk'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result": "success"
  }
```

친구와 헤어지기 요청을 전송합니다.

### HTTP 요청

`POST http://apis.dkdk.io/v1/dkdk`

### URL 파라메터

파라메터 | 설명
--------- | -----------
dkdk-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
user_uuid | 개발자 등록시 부여받은 user_uuid를 입력합니다.
action | 'bye'을 입력합니다.
friend_uuid | 친구요청 전송에 성공했을때 수신한 friend_uuid를 입력합니다.


#두근거림 보내고 받기

## 두근거림 패턴 보내기


```shell

curl -H "dkdk-token: DKDKTOKEN" -H "Content-type: application/json" -X POST -d '{"user_uuid":"USER_UUID", "action":"touch", "friend_uuids":["FRIEND_UUID_1","FRIEND_UUID_2"], "pattern_uuid" : "PATTERN_UUID"}' http://api.dkdk.io/v1/dkdk

```

```php

$body['action'] = 'touch';
$body['user_uuid'] = 'USER_UUID';
$body['pattern_uuid'] = 'PATTERN_UUID';
$body['friend_uuids'] = array("FRIEND_UUID_1", "FRIEND_UUID_2");

$headers = array(
        'Content-Type: application/json',
        'dkdk-token: DKDKTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.dkdk.io/v1/dkdk');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "touch", "user_uuid" : "USER_UUID", "pattern_uuid" : "PATTERN_UUID", "friend_uuids" : ["FRIEND_UUID_1", "FRIEND_UUID_2"]};

$.ajax({url : "https://api.dkdk.io/v1/dkdk",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("dkdk-token", "DKDKTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'dkdk-token' : 'DKDKTOKEN'
}
data = {
    'action': 'touch',
    'user_uuid' : 'USER_UUID',
    'pattern_uuid' : 'PATTERN_UUID',
    'friend_uuids' : ['FRIEND_UUID_1', 'FRIEND_UUID-2']
}

url = 'https://api.dkdk.io/v1/dkdk'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success"
  }
```

친구에게 나의 두근거림을 전송합니다.

### HTTP 요청

`POST http://apis.dkdk.io/v1/dkdk`

### URL 파라메터

파라메터 | 설명
--------- | -----------
dkdk-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
user_uuid | 개발자 등록시 부여받은 user_uuid를 입력합니다.
action | 'touch'를 입력합니다.
friend_uuids | 두근거림을 전송할 친구의 user_uuid를 입력합니다. (배열)
pattern_uuid | 두근거림의 패턴 pattern_uuid를 입력합니다.(두근거림 패턴 등록하기 참고) (Optional)


## 두근거림 전송을 중지하기


```shell

curl -H "dkdk-token: DKDKTOKEN" -H "Content-type: application/json" -X POST -d '{"user_uuid":"USER_UUID", "action":"up", "friend_uuids":["FRIEND_UUID_1", "FRIEND_UUID_2"}' http://api.dkdk.io/v1/dkdk

```

```php

$body['action'] = 'up';
$body['user_uuid'] = 'USER_UUID';
$body['friend_uuids'] = array("FRIEND_UUID_1", "FRIEND_UUID_2");

$headers = array(
        'Content-Type: application/json',
        'dkdk-token: DKDKTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.dkdk.io/v1/dkdk');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "up", "user_uuid" : "USER_UUID", "friend_uuids" : ["FRIEND_UUID_1", "FRIEND_UUID_2"]};

$.ajax({url : "https://api.dkdk.io/v1/dkdk",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("dkdk-token", "DKDKTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'dkdk-token' : 'DKDKTOKEN'
}
data = {
    'action': 'up',
    'user_uuid' : 'USER_UUID',
    'friend_uuids' : ['FRIEND_UUID_1', 'FRIEND_UUID_2']
}

url = 'https://api.dkdk.io/v1/dkdk'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success"
  }
```

친구에게 보내던 두근거림의 전송을 중지합니다

### HTTP 요청

`POST http://apis.dkdk.io/v1/dkdk`

### URL 파라메터

파라메터 | 설명
--------- | -----------
dkdk-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
user_uuid | 개발자 등록시 부여받은 user_uuid를 입력합니다.
action | 'up' 입력합니다.
friend_uuids | 두근거림을 전송하던 친구들의 user_uuid (배열)


#두근거림 등록/가져오기/삭제하기

## 두근거림 패턴 등록하기


```shell

curl -H "dkdk-token: DKDKTOKEN" -H "Content-type: application/json" -X POST -d '{"user_uuid":"USER_UUID", "action":"patternupload", "pattern":[0,100,5,100], "pattern_name" : "MY PATTERN NAME"}' http://api.dkdk.io/v1/dkdk

```

```php

$body['action'] = 'patternupload';
$body['user_uuid'] = 'USER_UUID';
$body['pattern'] = array(0,100,5,100);
$body['pattern_name'] = 'MY PATTERN NAME';

$headers = array(
        'Content-Type: application/json',
        'dkdk-token: DKDKTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.dkdk.io/v1/dkdk');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"action": "patternupload", "user_uuid" : "USER_UUID", "pattern" : [0,100,5,100], "pattern_name" : "MY PATTERN NAME"};

$.ajax({url : "https://api.dkdk.io/v1/dkdk",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("dkdk-token", "DKDKTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'dkdk-token' : 'DKDKTOKEN'
}
data = {
    'action': 'patternupload',
    'user_uuid' : 'USER_UUID',
    'pattern' : [0,100,5,100],
    'pattern_name' : 'MY PATTERN NAME'
}

url = 'https://api.dkdk.io/v1/dkdk'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success"
  }
```

나의 두근거림 패턴을 등록합니다.

### HTTP 요청

`POST http://apis.dkdk.io/v1/dkdk`

### URL 파라메터

파라메터 | 설명
--------- | -----------
dkdk-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
user_uuid | 개발자 등록시 부여받은 user_uuid를 입력합니다.
action | 'patternupload'를 입력합니다.
pattern | 진동패턴 배열을 입력합니다.(배열)('https://developer.android.com/reference/android/os/Vibrator.html'의 내용 참조)
pattern_name | 패턴의 이름을 입력합니다.


## 두근거림 패턴 가져오기


```shell

curl -H "dkdk-token: DKDKTOKEN" -H "Content-type: application/json" -X POST -d '{"user_uuid":"USER_UUID", "action":"pattern", "friend_uuid":"FRIEND_UUID", "pattern_uuid":"PATTERN_UUID"}' http://api.dkdk.io/v1/dkdk

```

```php

$body['action'] = 'pattern';
$body['user_uuid'] = 'USER_UUID';
$body['friend_uuid'] = 'FRIEND_UUID';
$body['pattern_uuid'] = 'PATTERN_UUID';

$headers = array(
        'Content-Type: application/json',
        'dkdk-token: DKDKTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.dkdk.io/v1/dkdk');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"user_uuid":"USER_UUID", "action":"pattern", "friend_uuid":"FRIEND_UUID", "pattern_uuid":"PATTERN_UUID"};

$.ajax({url : "https://api.dkdk.io/v1/dkdk",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("dkdk-token", "DKDKTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'dkdk-token' : 'DKDKTOKEN'
}
data = {
    'action': 'pattern',
    'user_uuid' : 'USER_UUID',
    'friend_uuid' : 'FRIEND_UUID',
    'pattern_uuid' : 'PATTERN_UUID'
}

url = 'https://api.dkdk.io/v1/dkdk'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success",
    "pattern":[0,100,2,100],
    "pattern_uuid":"PATTERN_UUID",
    "pattern_name":"PATTERN_NAME"
  }
```

친구의 두근거림 패턴을 내려 받습니다.

### HTTP 요청

`POST http://apis.dkdk.io/v1/dkdk`

### URL 파라메터

파라메터 | 설명
--------- | -----------
dkdk-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
user_uuid | 개발자 등록시 부여받은 user_uuid를 입력합니다.
action | 'pattern' 입력합니다.
friend_uuid | 두근거림 패턴을 가지고 있는 친구의 user_uuid
pattern_uuid | 내려받을 두근거림 패턴의 pattern_uuid

### 응답

파라메터 | 설명
--------- | -----------
pattern | 진동 패턴 (배열)
pattern_uuid | 두근거림 패턴의 pattern_uuid
pattern_name | 두근거림 패턴의 이름


## 두근거림 패턴 삭제하기


```shell

curl -H "dkdk-token: DKDKTOKEN" -H "Content-type: application/json" -X POST -d '{"user_uuid":"USER_UUID", "action":"patternremove", "pattern_uuid":"PATTERN_UUID"}' http://api.dkdk.io/v1/dkdk

```

```php

$body['action'] = 'patternremove';
$body['user_uuid'] = 'USER_UUID';
$body['pattern_uuid'] = 'PATTERN_UUID';

$headers = array(
        'Content-Type: application/json',
        'dkdk-token: DKDKTOKEN'
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.dkdk.io/v1/dkdk');
curl_setopt($ch, CURLOPT_HTTPHEADER,  $headers);
curl_setopt($ch, CURLOPT_POST,    true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS,json_encode($body));
$response = curl_exec($ch);
//$json_list= json_decode($response, true);
curl_close($ch);

echo $response;


```

```javascript

var jdata = {"user_uuid":"USER_UUID", "action":"patternremove", "pattern_uuid":"PATTERN_UUID"};

$.ajax({url : "https://api.dkdk.io/v1/dkdk",
       dataType : "json",
       contentType : "application/json",
       crossDomain: true,
       cache : false,
       data : JSON.stringify(jdata),
       type : "POST",
       async: false,
       beforeSend: function(request) {
          request.setRequestHeader("dkdk-token", "DKDKTOKEN");
        },
       success : function(r) {
         console.log(JSON.stringify(r));
         if(r.result == "success") {
           //r.data;
         }
       },
       error:function(request,status,error){
           alert("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
       }
});

```

```python

import requests
headers = {
    'Content-Type': 'application/json',
    'dkdk-token' : 'DKDKTOKEN'
}
data = {
    'action': 'patternremove',
    'user_uuid' : 'USER_UUID',
    'pattern_uuid' : 'PATTERN_UUID'
}

url = 'https://api.dkdk.io/v1/dkdk'
response = requests.post(url, headers=headers,
                         data=json.dumps(data))
response.raise_for_status()
'response.json()

```

> 상기의 명령은 아래와 같이 JSON 구조로 응답합니다:

```json
  {
    "result":"success"
  }
```

나의 두근거림 패턴을 삭제합니다.

### HTTP 요청

`POST http://apis.dkdk.io/v1/dkdk`

### URL 파라메터

파라메터 | 설명
--------- | -----------
dkdk-token | 부여받은 개발자 Token값을 헤더에 입력합니다.
user_uuid | 개발자 등록시 부여받은 user_uuid를 입력합니다.
action | 'patternremove' 입력합니다.
pattern_uuid | 삭제할 두근거림 패턴의 pattern_uuid