+++
title = "Scaling"
weight = "9"
+++

Now that you have the application data moved to an external service, we can safely scale our application up to more than one instance. After all, running a single instance of something is a recipe for an outage.

* Scale your app to two instances:

  ```sh
  cf scale first-push -i 2
  ```

  You should see output like:

  ```
  Scaling app first-push in org cloudfoundry-training / space development as steve@example.com...
  OK
  ```

#### Checking your work

You can see the status of your app by running `cf app first-push`:

```
Showing health and status for app first-push in org cff / space work as steve@example.com...

name:              first-push
requested state:   started
routes:            first-push-responsible-roan.<some-domain>
last uploaded:     Sun 31 Mar 11:47:05 MDT 2020
stack:             cflinuxfs3
buildpacks:        go

type:           web
instances:      2/2
memory usage:   64M
     state     since                  cpu    memory         disk          details
#0   running   2020-03-31T18:30:42Z   0.2%   10.2M of 64M   14.6M of 1G   
#1   running   2020-03-31T18:34:46Z   0.3%   9.5M of 64M    14.6M of 1G 
```

If you refresh your app in a browser multiple times, you will see the `App Instance Index` change (once the new instance has fully started and is available). Cloud Foundry is load balancing your requests across both instances.

### What happened?

Remember that image Cloud Foundry created when you pushed the app? Cloud Foundry grabbed a cached version of it and started a new container. When the app became available, Cloud Foundry started routing traffic to it. With multiple instances running, Cloud Foundry load balances traffic across them.

*And what didn't happen?*

Just like on a push, no creating resources. No updating routing tables. No updating load balancers.  Just `cf scale`.

Now that we have two instances running, let's crash one and see what happens.
