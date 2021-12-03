## 获取群组ID

## https://api.telegram.org/bot:xxxxxx/getUpdates

## To get the channel id

1. Create your bot with botfather
2. Make you bot an admin of your channel

## New improved next steps

1. Go to 电报的网页版
2. Click on your channel
3. Look at the URL and find the part that looks like `c12112121212_17878787878787878，点击频道，查看网页上的URL`
4. Remove the underscore and after `c12112121212 选择下划线前面部分`
5. Remove the prefixed letter `12112121212 去掉前面的英文前缀`
6. Prefix with a `-100` so `-10012112121212 加-100的前缀就是频道ID了，调用API时。chat_id填上频道ID就可以了。`
7. That's your channel id.

## Old yucky next steps

1. Make your channel public
2. Create a public link
3. Send a message from console to `@[your_public_link_text]`
4. Copy chat id from response in console as the channel id