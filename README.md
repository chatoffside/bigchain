# bigchain



## Steps

~~~
==> mkdir bigchain
~~~



~~~
==> cd bigchain
~~~

~~~
==> touch strongGenesis.json
~~~

Paste the contents
~~~
{
   "config": {
      "chainId": 2018,
      "homesteadBlock": 0,
      "eip155Block": 0,
      "eip158Block": 0,
      "byzantiumBlock": 0
   },
   "difficulty": "400",
   "gasLimit": "2000000",
   "alloc": {
      "7b684d27167d208c66584ece7f09d8bc8f86ffff": { 
          "balance": "100000000000000000000000" 
      },
      "ae13d41d66af28380c7af6d825ab557eb271ffff": { 
          "balance": "120000000000000000000000" 
      }
   }
}
~~~

Instantiate data directory

~~~
==> geth --datadir ./strongDataDir init ./strongGenesis.json
~~~

Start Ethereum peer node

~~~
==> geth --datadir ./strongDataDir --networkid 1114 console 2>> strongEth.log
~~~

In another terminal 

~~~
==> tail -f strongEth.log
~~~


In the geth Javascript console 
personal.newAccount("apple123")


Add another peer

~~~
==> geth --datadir ./peerDataDir init ./strongGenesis.json
~~~


Launch the 2nd peer on a different port 

~~~
==> geth --datadir ./peerDataDir --networkid 1114 --port 30304 console 2>> peerEth.log
~~~

~~~
==> tail -f peerEth.log 
~~~

In the 1st console

~~~
> admin.nodeInfo.enode
"enode://ae96f0115ebb17cbdb4494f04382233357c95a9fa5d293b75c2d24909f23dad5f9da03993deaed699cd9e69114e9a29fcf8a8a5c8fa49fb55085b91419b8e8b8@192.168.2.14:30303"
~~~

In the 2nd console

~~~
> admin.addPeer("enode://ae96f0115ebb17cbdb4494f04382233357c95a9fa5d293b75c2d24909f23dad5f9da03993deaed699cd9e69114e9a29fcf8a8a5c8fa49fb55085b91419b8e8b8@192.168.2.14:30303")
true
~~~

