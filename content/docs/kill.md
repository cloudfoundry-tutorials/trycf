+++
title = "Resiliency"
weight = "10"
+++

By performing `cf scale` in the last exercise, you asked Cloud Foundry to ensure you have two instances of the app running. Behind the scenes, Cloud Foundry is ensuring this is so. Let's test it.

To see this happen, we can watch the logs. We haven't talked about logs yet, but running `cf logs` will *tail* the logs for all of your application instances.

* In a terminal window, tail the logs:

  ```sh
  cf logs first-push
  ```

  You will see output similar to:

  ```
  Retrieving logs for app first-push in org cloudfoundry-training / space development as sgreenberg@rscale.io...

  ```

  This command doesn't run and exit. It keeps running, so it will not return to a command prompt. That is what we want.

The application has a `/kill` endpoint that will crash the instance programatically.

> **WARNING**: Don't build apps with a `/kill` endpoint! This for training purposes only.

* Go to your application in a browser. Tack on `/kill` to the URL and hit enter. You will see a `502 Bad Gateway` error as you will have killed this instance.

* Switch back to the terminal window where you are tailing the logs. You should see that Cloud Foundry (very quickly) detects an instance is missing and creates a new one.

* In another terminal window, you can also see the state of the new instance by running:

  ```sh
  cf app first-push
  ```

* You can also continue to access your root application URL (not the `/kill` endpoint) and see that you are routed to the live, running instance. Once the new instance starts up, Cloud Foundry routes traffic to it.

* When you are ready, you can stop tailing the logs by hitting `CTRL-C`


### Cool, so what happened?

Cloud Foundry is constantly monitoring the actual count of the running application instances and comparing that number to the desired count. If it finds an issue, Cloud Foundry will correct it (in our case, by creating a new instance). And just like during scaling, when the new instance becomes available Cloud Foundry routes traffic to it.

*And what didn't happen?*

A lot. All apps get this level of care from Cloud Foundry. You don't have to do anything other than use Cloud Foundry.

Nice work! Before we wrap up, let's clean up.
