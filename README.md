Demo project for a Mono app on Cloud Foundry
=================================================

Run on Cloud Foundry
--------------------
You must set environment variables for the HOSTNAME and DOMAIN where the application will run. You could also derive these values at runtime by parsing these values out of VCAP_APPLICATION env variable, but this works for now as a proof of concept.

Here are some examples with the beta release of cf v6 cli, known as gcf during the beta period using run.pivotal.io as an example. Make sure you are logged in and targeted to a space.

Prereqs:
Login to CF
Target your org and space
Clone this repo and cd into that directory

Make sure to substitute your DOMAIN and HOSTNAME where appropriate.

```
$ gcf push nancy-demo-hosting-self -m 512 -n nancy-demo-hosting-self --no-start -b https://github.com/friism/heroku-buildpack-mono.git
$ gcf set-env nancy-demo-hosting-self DOMAIN cfapps.io
Setting env variable domain for app nancy-demo-hosting-self in org jbayer-normal-org / space development as jbayer+normal@gopivotal.com...
OK
$ gcf set-env nancy-demo-hosting-self HOSTNAME nancy-demo-hosting-self
Setting env variable hostname for app nancy-demo-hosting-self in org jbayer-normal-org / space development as jbayer+normal@gopivotal.com...
OK
$ gcf start nancy-demo-hosting-self
$ curl http://nancy-demo-hosting-self.cfapps.io
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN">
<html>
  <head>
    <title>Nancy - Static view served by self-host</title>
  </head>
  <body>
    <h1>Nancy self-hosted example running</h1>
    <h2>Example of deploying Heroku / Mono onto Heroku</h2>
    <p>
      This view was served by the Nancy (C#) self-host.
    </p>
    <ul>
      <li>Scheme: http</li>
      <li><strong>HostName: nancy-demo-hosting-self.cfapps.io</strong></li>
      <li>Port: 62873</li>
      <li>BasePath: </li>
      <li>Path: /</li>
    </ul>
    <a href="http://nancy-demo-hosting-self.cfapps.io/">http://nancy-demo-hosting-self.cfapps.io/</a><br/>
    <a href="http://nancy-demo-hosting-self.cfapps.io/testing">http://nancy-demo-hosting-self.cfapps.io/testing</a><br/>
    <hr/>
    For more details, visit:
    <a href="http://blog.benhall.me.uk">http://blog.benhall.me.uk</a><br/>
    <a href="https://github.com/BenHall/heroku-buildpack-mono">https://github.com/BenHall/heroku-buildpack-mono</a><br/>
</body>
</html>
```



Procfile
--------
Web specifies the command that executes to start the application. The path to Mono is specified within the Buildpack, but is put on the path.

Build locally
-------------
Warning: I have never run this locally, but these were from the original README.md. The instructions may work.

Before deploying your source code you will need to ensure that it builds locally. For example:

	$ xbuild Nancy.Demo.Hosting.Self.sln

To test running your application locally, execute the following:

	$ foreman start local
	

  
