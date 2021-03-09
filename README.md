<div align="center">
    <h1>Freenom：freenom域名自动续费 12</h>
    
[![Build Status](https://img.shields.io/badge/build-passed-brightgreen?style=for-the-badge)](https://scrutinizer-ci.com/g/luolongfei/freenom/build-status/master)
[![Php Version](https://img.shields.io/badge/php-%3E=7.2-brightgreen.svg?style=for-the-badge)](https://secure.php.net/)
[![Scrutinizer Code Quality](https://img.shields.io/badge/scrutinizer-9.31-brightgreen?style=for-the-badge)](https://scrutinizer-ci.com/g/luolongfei/freenom/?branch=master)
[![MIT License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=for-the-badge)](https://github.com/luolongfei/freenom/blob/master/LICENSE)

Documentation: [English version](https://github.com/luolongfei/freenom/blob/master/README_EN.md) | 中文版
</div>

[📃  前言](#--前言)

[🍭  效果](#--效果)

[🎁  事前准备](#--事前准备)

[📪  配置发信邮箱](#--配置发信邮箱)

[🚧  配置脚本](#--配置脚本)

[🎈  添加计划任务](#--添加计划任务)

[☕  验证](#--验证)

[🤣  本项目最简单的使用方法](#--本项目最简单的使用方法)

[🍺  信仰](#--信仰)

[❤  捐赠 Donate](#--捐赠-donate)

[📋  捐赠名单 Donate List](#--捐赠名单-donate-list)

[🌚  作者](#--作者)

[🎉  鸣谢](#--鸣谢)

[🥝  开源协议](#--开源协议)


### 📃  前言
众所周知，Freenom是地球上唯一一个提供免费顶级域名的商家，不过需要每年续期，每次续期最多一年。由于我申请了一堆域名，而且不是同一时段申请的，
所


FREENOM_USERNAME	freenom 账户	-	是	只支持邮箱账户，不支持也不打算支持第三方社交账户登录
FREENOM_PASSWORD	freenom 密码	-	是	某些特殊字符可能需要转义，在Github actions环境，请在除字母数字以外的字符前加上“\”，否则可能无法正确读取密码，此举是防止某些字符在shell命令行被解析，举个例子，比如我密码是fei.,:!~@#$%^&*?233-_abcd^$$，那么写到秘密变量时就应写为fei\.\,\:\!\~\@\#\$\%\^\&\*\?233\-\_abcd\^\$\$。而在普通VPS环境，则只用在密码中的“#”或单双引号前加“\”，请参考.env.example文件内的注释，应该没人会设置那么变态的密码吧
MULTIPLE_ACCOUNTS	多账户支持	-	否	多个账户和密码的格式必须是“<账户1>@<密码1>|<账户2>@<密码2>|<账户3>@<密码3>”，如果设置了多账户，上面的FREENOM_USERNAME和FREENOM_PASSWORD可不设置
MAIL_USERNAME	机器人邮箱账户	-	是	支持Gmail、QQ邮箱以及163邮箱，尽可能使用163邮箱或者QQ邮箱，而非之前推荐的Gmail。因为谷歌的安全机制，每次在新设备登录 Gmail 都会先被限制，需要手动解除限制才行，而Github Actions每次创建的虚拟环境都会分配一个新的设备IP，相当于每次都是从新设备登录Gmail，而我们不可能每次都去手动为Gmail解除登录限制，所以这种机制会导致无法发出通知邮件。具体的配置方法参考「 配置发信邮箱 」
MAIL_PASSWORD	机器人邮箱密码	-	是	Gmail填密码，QQ邮箱或163邮箱填授权码
TO	接收通知的邮箱	-	是	你自己最常用的邮箱，推荐使用QQ邮箱，用来接收机器人邮箱发出的域名相关邮件
MAIL_ENABLE	是否启用邮件推送功能	true	否	true：启用
false：不启用
默认启用，如果设为false，不启用邮件推送功能，则上面的MAIL_USERNAME、MAIL_PASSWORD、TO变量变为非必须，可不设置
TELEGRAM_CHAT_ID	你的chat_id	-	否	通过发送/start给@userinfobot可以获取自己的id
TELEGRAM_BOT_TOKEN	你的Telegram bot的token	-	否	
TELEGRAM_BOT_ENABLE	是否启用Telegram Bot推送功能	false	否	true：启用
false：不启用
默认不启用，如果设为true，则必须设置上面的TELEGRAM_CHAT_ID和TELEGRAM_BOT_TOKEN变量
NOTICE_FREQ	通知频率	1	否	0：仅当有续期操作的时候
1：每次执行
