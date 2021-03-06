## Keys

we need to create public and private keys with ed25519

eg: public key
```
{
   "keyid_hash_algorithms":[
      "sha256",
      "sha512"
   ],
   "keyval":{
      "public":"fdba7eaa358fa5a8113a789f60c4a6ce29c4478d8d8eff3e27d1d77416696ab2"
   },
   "keytype":"ed25519"
}
```

eg: private key
 
```
7f8fcae94b95a04baa1f07aa374937f9@@@@100000@@@@48d5bd2502df5d921e714f0782f42e1df1ae08ffb4d0dbf5df1923557096b005@@@@a724429acda285bfb3e7f2b4db0b0928@@@@f6056beade9cd29b105c8f82186b24f5e9257a11420ddf2e4056a6ce7907ffb334dc130c6f12268f0229a5b34364d6375cd398de2b3aea93f6fd55355a725b8352caea89a625bf020e7a2a165aec5f95794f73265779056f9e3a227469cf89f484ff4067e4fa50241492810c89a5a9e83945af92a41a37096068f7fd01976ec209c3156bfc9308c5e95a1381859bff06a62df2ad2aabb9f417e2588941b9239d6a6d130572de94813cfd089eefbe73fe59e297f047dac67e8dfa437360bbc7ec953a507ca69fc48a21dadb6124643f6bf3e813d603a5609391cf5c1b5b30321a3024f3a8f97f325e96be102d0dceba28bf1f5a4c7614c0e0ffd2b6819758e0d02ad1df6adb16e23282dc502a
```

Each and very role will have the private and public pair

Each JSON file will have 2 segments `signatures` and `signed`

## ROOT.JSON

#### signatures

```
{
   "signatures":[
      {
         "keyid":"fdba7eaa358fa5a8113a789f60c4a6ce29c4478d8d8eff3e27d1d77416696ab2",
         "method":"ed25519",
         "sig":"dcbe4f76589cab2182dea476128ea7443a8116ede6ae044b80136ee3a0dbaa9bf0ed83f5d67b2e40fafbaac4ba9e513804f8cce4b842745ff0a58dc5f327b205"
      }
   ],
}
```

- Root Public key keyval ->> hexa code
- Root Private will generate signature ->> signatures `sig`

#### signed

- `_type` defines the actual role file. here is root
- `keys` - 4 types of keys for 4 roles along with hash algorithms, key type and key val -> pub of each roles
- signature->keyid === signed->keys->[] === signed->roles->root->keyid  ----->>> how this key is generated ---->>> A hexadecimal value in '23432df87ab..' format `SCHEMA.RegularExpression(r'[a-fA-F0-9]+')`
- threshold - no. of keyids pair are there for verification
- version - no of time the `root.json` file has changed
- `root.json` file change only if keys or signature is changed

```
{
   "signed":{
      "_type":"Root",
      "compression_algorithms":[
         "gz"
      ],
      "consistent_snapshot":false,
      "expires":"2023-07-07T12:19:10Z",
      "keys":{
         "630cf584f392430b2119a4395e39624e86f5e5c5374507a789be5cf35bf090d6":{
            "keyid_hash_algorithms":[
               "sha256",
               "sha512"
            ],
            "keytype":"ed25519",
            "keyval":{
               "public":"99ef8790687ca252c4677a80a34e401efb7e17ccdf9b0fcb5f1bc3260c432cb9"
            }
         },
         "da9c65c96c5c4072f6984f7aa81216d776aca6664d49cb4dfafbc7119320d9cc":{
            "keyid_hash_algorithms":[
               "sha256",
               "sha512"
            ],
            "keytype":"ed25519",
            "keyval":{
               "public":"d1ab5126fd6f0e30944910e81c0448044dfe9d5a39f478212b2afa913bb7ca7c"
            }
         },
         "f93cfcf33d335ff43654ec6047e0a18dd5595ee3de53136b94c9c756788a0f97":{
            "keyid_hash_algorithms":[
               "sha256",
               "sha512"
            ],
            "keytype":"ed25519",
            "keyval":{
               "public":"228342cc8b78a65b8840ef5691a693d8c368e053a7e8e8f85faf7c83eff1e1d2"
            }
         },
         "fdba7eaa358fa5a8113a789f60c4a6ce29c4478d8d8eff3e27d1d77416696ab2":{
            "keyid_hash_algorithms":[
               "sha256",
               "sha512"
            ],
            "keytype":"ed25519",
            "keyval":{
               "public":"f3b4c231520580eca92e17ae1581a708f606f72d43cc200af493afeec22a5e79"
            }
         }
      },
      "roles":{
         "root":{
            "keyids":[
               "fdba7eaa358fa5a8113a789f60c4a6ce29c4478d8d8eff3e27d1d77416696ab2"
            ],
            "threshold":1
         },
         "snapshot":{
            "keyids":[
               "f93cfcf33d335ff43654ec6047e0a18dd5595ee3de53136b94c9c756788a0f97"
            ],
            "threshold":1
         },
         "targets":{
            "keyids":[
               "630cf584f392430b2119a4395e39624e86f5e5c5374507a789be5cf35bf090d6"
            ],
            "threshold":1
         },
         "timestamp":{
            "keyids":[
               "da9c65c96c5c4072f6984f7aa81216d776aca6664d49cb4dfafbc7119320d9cc"
            ],
            "threshold":1
         }
      },
      "version":1
   }
}
```

## TARGET.JSON

#### signature

```
"signatures": [
  {
   "keyid": "630cf584f392430b2119a4395e39624e86f5e5c5374507a789be5cf35bf090d6",
   "method": "ed25519",
   "sig": "3bcf3ced34e24c02c1e872d2fe7dc93b01cf2e8474a609231f398c3ca31d3dcaa3a1f32d2c70a89404d981f355dd13f3bf88fc0be89e6ccde14a549e38695900"
  }
 ],
 ```
- Target keyid ->> hexa code
- Target Private will generate signature ->> signatures `sig`
- Target's keyid is stored in `root.json` under signed object

#### Signed

```
"signed": {
  "_type": "Targets",
  "delegations": {
   "keys": {},
   "roles": []
  },
  "expires": "2022-10-06T13:58:00Z",
  "targets": {
   "/ota.txt": {
    "custom": {
     "ecu_serial": "TCUdemocar"
    },
    "hashes": {
     "sha256": "0b016a3bc4d9e2b7368497772d958a7a5063ba8bf57cae0a8603ada5aef8ae3f",
     "sha512": "ea933feee0f5377223e6904d8c8914f5d4ee165bdec15b33189b58d26b9b1b0384c4e785fbf928733d0c1a810b765479455e5ca1c5bb2a1303ce1ad200f11b94"
    },
    "length": 18
   }
  },
  "version": 2
 }
```

- `_type` defines the actual role file. here is target
- `targets` - all targets for repo will be stored under this along with target hashes
- version - no of time the `root.json` file has changed
- `target.json` file change only if new target is mapped for any ECU and version also changes at that time
- `targets` -> filename -> custom -> ecu_serial - ECU id where the software needs to be installed
- `targets` -> filename -> hashes - hash key of the uploaded image in 2 formats sha256 & sha512
- `targets` -> filename -> length - length of the uploaded file 


## SNAPSHOT.JSON

#### Signature

```
"signatures": [
  {
   "keyid": "f93cfcf33d335ff43654ec6047e0a18dd5595ee3de53136b94c9c756788a0f97",
   "method": "ed25519",
   "sig": "05411d6e42e2193db983c5d1d554ba50bc7f72ce60f6e0c499e3b8979b6058f6968e8d109795669cf49edfc2f1614a3a0cfd9310d5899ff5f8cb878e31d46f0b"
  }
 ],
```

- Snapshot keyid ->> hexa code
- Snapshot Private key will generate signature ->> signatures `sig`
- Snapshot's keyid is stored in `root.json` under signed object

#### Signed

```
"signed": {
  "_type": "Snapshot",
  "expires": "2022-07-14T06:30:50Z",
  "meta": {
   "root.json": {
    "hashes": {
     "sha256": "d80ac46893407d2948efb26a6231e727777a719da3f01a96678bd940222be9cd"
    },
    "length": 2120,
    "version": 1
   },
   "targets.json": {
    "version": 2
   }
  },
  "version": 2
 }
```

- `_type` defines the actual role file. here is snapshot
- `snapshot.json` file will change only if `root.json` or `target.json` changes
- `meta` -> filename -> hashes - hash key of the uploaded file in sha256 format
- `meta` -> filename -> length - length of the uploaded file 
- `meta` -> filename -> version - version of the uploaded file 


## TIMESTAMP.JSON

#### Signature

```
"signatures": [
  {
   "keyid": "da9c65c96c5c4072f6984f7aa81216d776aca6664d49cb4dfafbc7119320d9cc",
   "method": "ed25519",
   "sig": "8fce77f1d2f20d5ecb4f146ad2cb80af80c6aacd88cf479791d3e60eb778aaf32de0bc72b0302679cbc7aae18ad0362d1e683eae264a46bb06a297a457938800"
  }
 ],
```

- Timestamp keyid ->> hexa code
- Timestamp Private key will generate signature ->> signatures `sig`
- Timestamp's keyid is stored in `root.json` under signed object

#### Signed

```
"signed": {
  "_type": "Timestamp",
  "expires": "2022-07-08T06:30:50Z",
  "meta": {
   "snapshot.json": {
    "hashes": {
     "sha256": "9bd8ef8308e876d44b1ccd491dc81459cb3565baae594152d71da81035cfef53"
    },
    "length": 594,
    "version": 2
   }
  },
  "version": 2
 }
```

- `_type` defines the actual role file. here is timestamp
- `timestamp.json` file will change only if `snapshot.json` changes
- `meta` -> filename -> hashes - hash key of the uploaded file in sha256 format
- `meta` -> filename -> length - length of the uploaded file 
- `meta` -> filename -> version - version of the uploaded file 
- this file will be first download on verification process


## Verification flow

- timestamp.json
- snapshot.json
- target.json
- root.json (download this root.json file when verification fails at any point)

