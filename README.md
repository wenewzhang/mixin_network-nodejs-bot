# Howto create nodejs bot for Mixin Network step by step
Mixin Network is a cryptocurrency payment which confirm the transactions instantly,  users can deposit, withdraw and pay bitcoin or altcoins through [Mixin Messenger](https://mixin.one/),
the developers could earn money from the user's exchanges. It's a excellent ecosystem.

This article will show you howto create a nodejs-bot

### First of all, install npm node on your OS
mac OS
```
brew install node npm
```

Ubuntu
```
apt update
apt upgrade
apt install node npm
```
if your npm and node are too old, execute **npm i npm/node** to upgrade npm-self and node
```
npm i node
npm i npm
```

### Then, create you first bot through [Mixin.One](https://developers.mixin.one/dashboard),if you get a "Invaild Data" message,Just finish all the required options.
write down three required infomations: user id, session id, private key, mixin-node sign the token with them.

| Key | Description                                  |   example                                         |
| --- | -------------------------------------------- |  -------------------------------------------------
| user id | unique bot identity, uuid,for token signature | 21042518-85c7-4903-bb19-f311813d1f51          |
| session id | session identity, uuid,for token signature | 5eb96d87-028e-4199-a6d3-6fc7da8dfe41          |
| private key | RSA private key for token signature  | -----BEGIN RSA PRIVATE KEY----- -----END RSA PRIVATE KEY-----


![mixin_network-keys](https://github.com/wenewzhang/mixin_network-nodejs-bot/blob/master/mixin_network-keys.png)
Open the terminal and go to the workspace, make nodejs-bot directory
```
mkdir nodejs-bot
cd nodejs-bot/
npm init
```
run **npm init** command then according the prompt to create the project, the finished package.json is like below:
```
{
  "name": "nodejs-bot",
  "version": "1.0.0",
  "description": "nodejs bot for mixin network",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "jimmyzhang",
  "license": "ISC"
}
```
this example dependents on mixin-node SDK and koa,
```
const mixinjs = require("mixin-node");
const Koa = require('koa');
```
execute **npm install mixin-node** to add the packages
```
npm install koa mixin-node
```
now,the package.json add two packages
```
"dependencies": {
  "koa": "^2.6.2",
  "mixin-node": "^1.0.24"
}
```

### The next, source code brief explanation
Initial the connection and sign the token.
> app.js
```
const config = require("./config");
let opts = config.mixin;
let mixin = new mixinjs(opts);
```
process the incoming message
```
mixin.onMessage = (data) => {
...
};
```
answer the question **pay**
```
let textEventHandle = (msgobj) => {
    if (msgobj.data.data == "pay") {
      ...
      }
    }
}
```
open config.js, replace your client_id with user id, session_id with session id,
open mixin_dev.key, replace the private key with your's.
> config.js
```
config.mixin = {
  client_id: "21042518-85c7-4903-bb19-f311813d1f51",
  session_id: "5eb96d87-028e-4199-a6d3-6fc7da8dfe41",
  privatekey: "mixin_dev.key"
}
```
### Finally, you can run **node app.js** to take the bot online.
```
node app.js
```

install [Mixin Messenger](https://mixin.one/),add the bot as your friend,(for example, this bot id is 7000101639) and then send command!
enjoy!

![mixin_messenger](https://github.com/wenewzhang/mixin_network-nodejs-bot/blob/master/mixin_messenger-bot.jpeg)
