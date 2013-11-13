Demo project for hosting Nancy and Mono on Cloud Foundry
=================================================

Build locally
-------------
Before deploying your source code you will need to ensure that it builds locally. For example:

	$ xbuild Nancy.Demo.Hosting.Self.sln

Run on Cloud Foundry
--------------------
You must set environment variables for the hostname and domain where the application will run.

Here are some examples with the beta release of cf v6 cli, known as gcf during the beta period using run.pivotal.io as an example.

```
$ gcf push nancy-demo-hosting-self -m 512 -n someavailablehostname --no-start
$ gcf set-env nancy-demo-hosting-self DOMAIN cfapps.io
Setting env variable domain for app nancy-demo-hosting-self in org jbayer-normal-org / space development as jbayer+normal@gopivotal.com...
OK
$ gcf set-env nancy-demo-hosting-self HOSTNAME someavailablehostname
Setting env variable hostname for app nancy-demo-hosting-self in org jbayer-normal-org / space development as jbayer+normal@gopivotal.com...
OK
$ gcf start nancy-demo-hosting-self
```

Note that it is mandatory to set the environment variables for hostname and domain. You could also derive these values at runtime by parsing these values out of VCAP_APPLICATION env variable, but this works for now as a proof of concept.

Procfile
--------
Web specifies the command that executes to start the application. The path to Mono is specified within the Buildpack, but is put on the path.

To test running your application locally, execute the following:

	$ foreman start local
  
