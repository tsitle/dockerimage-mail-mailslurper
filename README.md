# MailSlurper Docker Image for AARCH64, ARMv7l, X86 and X64

Provides MailSlurper, which is a handy SMTP mail server useful for local
and team application development.  
You can use this image to send mail to a SMTP host
and MailSlurper provides the SMTP server and web frontend.  
For more information on MailSlurper please see MailSlurper [website](http://mailslurper.com/) and [Wiki](https://github.com/mailslurper/mailslurper/wiki).

## Docker Container usage
See the related GitHub repository [https://github.com/tsitle/dockercontainer-mail-mailslurper](https://github.com/tsitle/dockercontainer-mail-mailslurper)

## Source of MailSlurper binary packages
The binary packages were built using 
[https://github.com/tsitle/dockercontainer-app-go\_native\_compiler](https://github.com/tsitle/dockercontainer-app-go_native_compiler)  
and the build script `build-mailslurper.sh` that the repository contains.

## Configuration
[Server Settings](CONFIG_SERVER.md)  
Source: [https://github.com/mailslurper/mailslurper/wiki/Server-Configuration](https://github.com/mailslurper/mailslurper/wiki/Server-Configuration)

[Using a SQL-Server](CONFIG_SQLSERVER.md)  
Source: [https://github.com/mailslurper/mailslurper/wiki/Using-A-SQL-Server](https://github.com/mailslurper/mailslurper/wiki/Using-A-SQL-Server)
