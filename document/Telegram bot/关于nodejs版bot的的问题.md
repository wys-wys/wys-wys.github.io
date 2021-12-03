在模仿做发送图片的机器的的时候，

```js
const TelegramBot = require('node-telegram-bot-api');
const Agent = require('socks5-https-client/lib/Agent');
const request = require('request');

const token = '填入你的token';
const bot = new TelegramBot(token, {
  polling: true,
  request: { // 设置代理
    agentClass: Agent,
    agentOptions: {
      socksPassword: '填入你登梯子时的密码'
    }
  }
});


bot.onText(/\/hentai/, function onLoveText(msg) {
  bot.sendMessage(msg.chat.id, 'Are you a hetai?');
});

bot.onText(/\/prpr/, function onLoveText(msg) {
  const chatId = msg.chat.id;
  request('https://konachan.com/post.json?tags=ass&limit=50', function (error, response, body) {
    if (!error && response.statusCode == 200) {
      const result = JSON.parse(body) || [];
      const index = parseInt(Math.random() * result.length);
      bot.sendPhoto(chatId, result[index].file_url, { caption: '手冲一时爽，一直手冲一直爽' }).catch((err) => {
        bot.sendMessage(chatId, '手冲失败');
      })
    } else {
      bot.sendMessage(chatId, '手冲失败');
    }
  });
});


bot.onText(/\/echo (.+)/, (msg, match) => {

  const chatId = msg.chat.id;
  const resp = match[1];
  bot.sendMessage(chatId, resp);
});
```

由于涂省事只复制了发送图片的代码段

折腾了好久一直不能发送图片 ，请求失败，后来自己百度了request的用法发现需要首先

定义一个request ，真坑啊，没看清

```
const request = require('request');
```

