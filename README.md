# MailSlurper Docker Image for AARCH64, ARMv7l, X86 and X64

Provides MailSlurper, which is a handy SMTP mail server useful for local
and team application development.  
You can use this image to send mail to a SMTP host
and MailSlurper provides the SMTP server and web frontend.  
For more information on MailSlurper please see MailSlurper [website](http://mailslurper.com/) and [Wiki](https://github.com/mailslurper/mailslurper/wiki).

## Docker Container usage
The image contains a default MailSlurper config file (`/opt/mailslurper/config.json`).  
A custom config file can be used by mounting an external file into the container.

Run the image using:

```
$ docker run \
		--rm \
		-d \
		-v $PWD/custom-config.json:/opt/mailslurper/config.json \
		-p 2500:2500 \
		-p 8080:8080 \
		-p 8085:8085 \
		mail-mailslurper
```

## Email Client configuration
- SMTP port: 2500
- SMTP Authentification required?: no
- SMTP via SSL or TLS?: no

## Web Frontend usage
Navigate to `http://localhost:8080` in your webbrowser.
