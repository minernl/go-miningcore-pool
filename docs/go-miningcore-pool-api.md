# Go-Miningcore-Pool API
Miningcore Pool API

### Path `/config`


all available configs 

```javascript
[
    "/config/ports", "/config/coin", "/config/api"
]
```

## Path "/config/ports"

GET

```json
[
    {
        "host": "192.168.1.101",
        "port": 10086,
        "ssl": true,
        "algorithm": {
        "name": "scrypt",
        "variant": "ltc-origin",
        "blobType": ""
        },
        "difficulty": 0.02,
        "fee": 0,
        "desc": "Low-End Cpu and Gpu"
    },
    {
        "host": "192.168.1.102",
        "port": 10088,
        "ssl": true,
        "algorithm": {
        "name": "scrypt",
        "variant": "ltc-origin",
        "blobType": ""
        },
        "difficulty": 2,
        "fee": 0,
        "desc": "High-End rigs"
    }
]
```



## Path "/pool"

GET

Stats shows the pool basic mining status.

```javascript
{
    "minerCount": 10,
    "rigCount": 20,
    "totalMined": 14,
    "totalHashrates": 3366733275,
    "totalDiff":9506129270212336,
    "totalShares":8918601904388584,
}
```

## Path "/pool/network"

GET

```javascript

{
    "height": 1187802,
    "hashrate": 3366733275,
    "difficulty": 538996687554816,
}
```

### Path "/pool/blocks"

- GET/POST

on default, return 25 items as maximum

Can also POST with limitation

Get all blocks mined between 1-Jan-2022 and 10-Jan-2022

```javascript
{
  "from": "1-Jan-2022",
  "to": "10-Jan-2022"
}
```

Get 100 mined blocks from 1-Jan-2022

```javascript
{
  "from": "1-Jan-2022",
  "max": 100, // "max" will be ignored when having a "to"
}
```

Get last(latest) 100 blocks mined by pool

```javascript
{
  "max": 100, // "max" will be ignored when having a "to"
}

```

the return looks like this

```javascript
[
  {
    "difficulty": 539702861270356,
    "hash": "8d04b7f92faba60fdc071304c1d1260daed0dd6a30def76dc3e322589b867762",
    "height": 1187801,
    "reward": 4129400000000,
    "timestamp": 1582458302
  },
  {
    "difficulty": 539702861270356,
    "hash": "8d04b7f92faba60fdc071304c1d1260daed0dd6a30def76dc3e322589b867762",
    "height": 1187801,
    "reward": 4129400000000,
    "timestamp": 1582458302
  },
  {
    "difficulty": 539702861270356,
    "hash": "8d04b7f92faba60fdc071304c1d1260daed0dd6a30def76dc3e322589b867762",
    "height": 1187801,
    "reward": 4129400000000,
    "timestamp": 1582458302
  }
]
```

### Path "/pool/blocks/last"

- Get

last Block Mined

```javascript
[
  {
    "difficulty": 539702861270356,
    "hash": "8d04b7f92faba60fdc071304c1d1260daed0dd6a30def76dc3e322589b867762",
    "height": 1187801,
    "reward": 4129400000000,
    "timestamp": 1582458302
  },
  // ...
]
```


## GET "/miner/{miner}"

get the details of miner

## POST "/miner/{miner}"

submit the additional miner options to pool, like payment method

```json

{
    "totalAverageHashrate": 18000, // unit h/s
    "totalLiveHashrate": 18000,
    "lastShareTimestamp": 1582801903,
    "rigs": ["rig1", "rig2", "rigN"]
}

```

## GET "/miner/{miner}/{rig}"

get the stats of rig


# Objects

## Algorithm

```javascript
{
    "name": "scrypt",
    "variant": "ltc-origin", // an additional remark for algorithm name
    "blobType": "bitcoin" // maybe cryptonote v1/v2, forknote v1/v2, ethereum or any other coin's own blobType, just used as an additional remark for variant. Pool software can keep null or "".
}
```

## Port

port is an object contains the configs for guiding users to quick start mining on your pool

```javascript
{
    "host": "192.168.1.101",
    "port": 10086,
    "algorithm": {
        "name": "scrypt",
        "variant": "ltc-origin",
        "blobType": ""
    },
    "ssl": true,
    "difficulty": 0.02,
    "fee": 0,
    "desc": "Low-End Cpu and Gpu"
}
```

## Block

```javascript
{
    "difficulty": 539702861270356, // float64
    "hash":"8d04b7f92faba60fdc071304c1d1260daed0dd6a30def76dc3e322589b867762",
    "height": 1187801,
    "reward": 4129400000000,
    "timestamp": 1582458302
}
```





























