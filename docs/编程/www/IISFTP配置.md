IIS + FTP配置时，本地始终连接不上，不管是主动还是被动方式。

无限次折腾后发现，原来把服务器重启一下就好了。看样子是FTP配置改动后，并不是立即生效。需要重启才行。

如果选择被动方式，最好是指定一下FTP服务器使用的端口范围。不然可能会被安全组限制。要在安全组中相应开通端口。