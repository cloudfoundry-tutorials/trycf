+++
title = "Login and Target"
weight = "4"
+++

When using Cloud Foundry, the first thing you need to do is log in to a Cloud Foundry instance.  To log in, you will run the following:

```sh
cf login -a <CLOUDFOUNDRY_API_ENDPOINT> -u <USERNAME>
```

Let's break it down.  

* The `-a` flag allows you to specify the API endpoint of the Cloud Foundry instance you are using. Each instance of Cloud Foundry will have its own unique API endpoint or URL. Here are the API endpoints by provider (if you are using a different provider, you can get the API endpoint from that provider):

| Provider              | API Endpoint                               			|
|-----------------------|-------------------------------------------------|
| anynines    					| https://api.de.a9s.eu                      			|
| cloud.gov		          | https://api.fr.cloud.gov             					 	|
| IBM Cloud    					| *varies. see https://console.bluemix.net/docs/*	|
| Pivotal Web Services  | https://api.run.pivotal.io                 			|
| Swisscom              | https://api.lyra-836.appcloud.swisscom.com 			|

* The `-u` flag allows you to specify your username for that Cloud Foundry instance. You can leave this flag off and the CLI will prompt you for your username.

* We purposely did not use the `-p` flag to provide your password in a single command. This flag exists but is intended for automation. Providing the password via a flag with the login command means your password will be in clear text in the terminal history. Therefore, it is better to only use `-p` for CI/CD systems and leave it off when using Cloud Foundry manually.

> Note: You can use `cf login --help` for details on all of the available flags you can specify.

#### Checking your work

If you log in successfully, you should see output similar to below:

```
Authenticating...
OK

Targeted org cloudfoundry-training

Targeted space development

API endpoint:   https://api.run.pivotal.io (API version: 2.103.0)
User:           sgreenberg@rscale.io
Org:            cloudfoundry-training
Space:          development
```

> Note the reference to the `Org` and `Space` above. Orgs and spaces are logical separations within a Cloud Foundry instance. For now, all you need to know is that apps are deployed to spaces. If you only have a role in one org and space, the CLI will default to use that one.

If you are logged in successfully, it's time to deploy an app!
