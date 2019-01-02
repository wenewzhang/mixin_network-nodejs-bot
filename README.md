# Howto create nodejs bot for Mixin Network step by step
Mixin Network is a cryptocurrency payment which confirm the transactions instantly,  users can deposit, withdraw and pay bitcoin or altcoins through [Mixin Messenger](https://mixin.one/),
the developers could earn money from the user's exchanges. It's a excellent ecosystem.

This article will show you howto create a nodejs-bot

### First of all,install npm node on your OS
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

### The next,source code brief explanation
Initial the connection and sign the token,
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
      mixin.sendText("Payment:", msgobj).then(function(receipt_id) {
      }
    }
}
```
### Finally,you can run **node app.js** to take the bot online.
```
node app.js
```

install [Mixin Messenger](https://mixin.one/),add the bot as your friend,(for example, this bot id is 7000101639) and then send command!

enjoy!
