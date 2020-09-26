# localbitcoin++
<strong>DISCLAIMER: This project is for educational purposes. Use of this software for commercial purpose is higly discouraged and shall be done on personal risk. The author shall not be deemed responsible for any profit or loss of any kind.</strong>

### About
A distributed single HTML page Bitcoin trading platform. Based on pure Javascript, this single page HTML 5 Bitcoin trading exchange can be used to deposit, withdraw and trade Bitcoins removing need to download any app or software. Moreover, this application also removes any need of username and password verification.

The application is currently in beta phase.

### Features
- buy, sell, deposit, withdraw Bitcoins and/or FLO; 
- exchange with fiat currencies;
- inbuilt decentralized wallet to store, send or receive Bitcoins and/or FLO;
- p2p architecture;
- powered by FLO blockchain;
- passwordless exchange;
- single HTML5 webpage application;

### Architecture
The same index.html file serves as both server and client. The base architecture is powered by [FLO](https://www.flo.cash/ "FLO") blockchain which is a fork of the bitcoin blockchain with a field to store about 1000 characters in blockchain. This field, called floData, is used to store rules for the exchange using a master Flo key. A sample master rules is given as follows:

```javascript
masterFLOPubKey=03EA5E2CAB18DA585400D6EC569438D415FAF200528E05D0E2B9BEAA2B5C3DCA90#!#tradableAsset1=BTC,FLO,BTC_TEST,FLO_TEST#!#tradableAsset2=INR,USD,#!#validTradingAmount=10,50,100,#!#btcTradeMargin=5000#!#MaxBackups=1#!#waitTime={"normaldelay":60000,"exportdelay":60000,"syncdelay":60000,"hugedelay":60000}#!#ordersLife={"trade":300000,"cryptoDeposit":900000,"cryptoWithdraw":300000,"cashDeposit":900000,"cashWithdraw":900000}#!#miners_fee={"btc":0.0005,"flo":0.001}#!#supernodesPubKeys=026FCC6CFF6EB3A39E54BEB6E13FC2F02C3A93F4767AA80E49E7E876443F95AE5F,0349B08AA1ABDCFFB6D78CD7C949665AD2FF065EA02B3C6C47A5E9592C9A1C6BCB,039B4AA00DBFC0A6631DE6DA83526611A0E6B857D3579DF840BBDEAE8B6898E3B6,0315C3A20FE7096CC2E0F81A80D5F1A687B8F9EFA65242A0B0881E1BA3EE7D7D53,03C8E3836C9A77E2AF03D4265D034BA85732738919708EAF6A16382195AE796EDF,03F7493F11B8E44B9798CD434D20FBE7FA34B9779D144984889D11A17C56A18742#!#specialNodes=02348523EB008BD37BF297AA360757062CB9D153C371EE727349A02F0B67910613,03C38E6523D6A2C45E00E60DC072E4D4340007F8A0026F134DCBBC670E4C44D31C#!#cashiers={"032871A74D2DDA9D0DE7135F58B5BD2D7F679D2CCA20EA7909466D1A6912DF4022":{"upi":"johnDoe@upi","currencies":["INR"],"is_live":false},"03DB4A12EB543B293DDBB0CE314C46C36D6761294AFBB7264A6D78F710FFD97CF0":{"upi":"janeDoe@upi","currencies":["INR","USD"],"is_live":false}}#!#ShamirsMaxShares=8#!#supernodeSeeds={"ranchimall1":{"ip":"127.0.0.1:9111","kbucketId":"oZxHcbSf1JC8t5GjutopWYXs7C6Fe9p7ps"},"ranchimall2":{"ip":"127.0.0.1:9112","kbucketId":"oTWjPupy3Z7uMdPcu5uXd521HBkcsLuSuM"},"ranchimall3":{"ip":"127.0.0.1:9113","kbucketId":"odYA6KagmbokSh9GY7yAfeTUZRtZLwecY1"},"ranchimall4":{"ip":"127.0.0.1:9114","kbucketId":"oJosrve9dBv2Hj2bfncxv2oEpTysg3Wejv"},"ranchimall5":{"ip":"127.0.0.1:9115","kbucketId":"oMhv5sAzqg77sYHxmUGZWKRrVo4P4JQduS"}"ranchimall6":{"ip":"127.0.0.1:9116","kbucketId":"oV1wCeWca3VawbBTfUGKA7Vd368PATnKAx"}}
```

The so called master comment contains various rules separated by a delimitter #!# in a key value pair to write rules for the exchange. For example, supernodeSeeds are the ip addresses of the various servers that form the p2p architecture. tradableAsset1 to set which crypto can be traded in the exchnage among BTC and FLO or both.

Once the master comment is broadcasted to the blockchain the servers described in supernodeSeeds can be started to instantiate the p2p network. Once the network is established each server connect to its n nearest neighbors according to XOR distances of their respective Flo addresses. This setup is important as each server also maintains data backup amongst their neighbors.

#### Run as a client
Once the servers started running the clients can connect to any one of these servers by just running the index.html page. Users will need to provide a Flo private key to login into the system. This private key must be stored securely and safely by the user as this is the key to their account into the exchange. Losing the private key means losing access to all your assets. Users can generate a Flo private key using the exchange itself or you can generate from [here](https://flo-webwallet.duckdns.org/ "here").

### Workflow
Once the user has successfully logged into the exchange the next thing he needs to do is to deposit crypto (BTC or FLO) and/or fiat currency. Once done, user can trade his assets against other.

There are primarily three tabs namely *Trade, Exchange *and* Cash*.

+ **Trade**
	+ Buy - fill and submit the form to buy Bitcoins
	+ Sell - fill and submit the form to sell Bitcoins 

+ **Crypto**
	+ Deposit to exchange - fill and submit the form to deposit Bitcoins
	+ Withdrawfrom exchange - fill and submit the form to withdraw Bitcoins
	+ Confirm deposit - optionally you can use this button to inform the server that you have deposited (sent) the bitcoins to the address given by the exchange during deposit process
	+ Send to any address - this is a inbuilt wallet to send bitcoins to a bitcoin address

+ **Cash**
	+ Deposit - fill and submit the form to deposit cash
	+ Withdraw - fill and submit the form to withdraw cash

There are other important sections:

The **Balance** section provides information about the current balance of the user both fiat and crypto. 

The **Market Price** provides information about the current trading price of the respective crypto.

The **My Orders** section provides information about status of the assets put on trade.

The **Activity** section can be used to learn about the current status of both crypto and fiat deposited or withdrawn.

The **User** section can be used to set default currency and logging out from the system.

