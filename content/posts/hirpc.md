---
title: Remote Procedure Calls (HiRPC)
weight: 4
---

# HiBON Remote Procedure Call (HiRPC)

HiRPC is a RPC which can including digital signatures and it is base on HiBON data format.

## Structure of HiRPC
```js
{
    $@ : 'HiPRC',
    $sign : <bin>, // Optional
    $pkey  : <bin>, // Optional
    $msg : {
        id : <uint>,
        method : <string>, // Name of the method
        params : <Document>, // Optional
    }
}
```
The member **sign** is the $sign **hirpc** object and **$pkey** is the public-key which also include a $sign schema code in the genetic package.

### Success full result
```js
{
    $@ : 'HiRPC',
    $sign : <bin>, // Optional
    $pkey : <bin>, // Optional
    $msg : {
        id : <uint>,
        result : <Document>
    }
}

```

### Failure result
```js
{
    $@ : 'HiRPC',
    $sign : <bin>, // Optional
    $pkey : <bin>, // Optional
    $msg : { // This part is signed
        id : <uint>,
        code : <uint>, // Optional
        message : <string> // Optional
	    data : <DOCUMENT> // Optional
    }
}
```
