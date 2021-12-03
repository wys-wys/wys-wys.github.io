### 一直提示telepot.exception.TelegramError: ('Bad Request: chat not found', 400, {'ok': False, 'error_code': 400, 'description': 'Bad Request: chat not found'})

- 原因，chat_id不是用户的username只能通过getupdates的方法获取用户的id和相关的信息，用获取到的id再sendmessage就没有问题了
- 

