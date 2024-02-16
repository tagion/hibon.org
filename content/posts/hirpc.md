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

The method may include a '.'.
Only the last string behind the dot is interpreted as the function name.
The string preceeding is an optional entity name.
Eg. tagion full nodes can take `<dartCRUD(RO)>` commands with no entity prefix to read from main dart. And `trt.<dartCRUD(RO)>` commands to read from the trt(transaction reverse table) dart.
See the [tagion hirpcmethods](https://docs.tagion.org/#/documents/protocols/contract/hirpcmethods) for more real world examples.

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
