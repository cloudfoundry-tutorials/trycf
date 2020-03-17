+++
title = "Cleanup"
weight = "11"
+++

Cleaning up with Cloud Foundry is simple.

```sh
# delete the app and the route
cf delete -f -r first-push

# delete the database instance
cf delete-service -f first-push-db
```

Congratulations! You just:

* Deployed an application to Cloud Foundry using `cf push`.
* Created a service instance from the marketplace (`cf marketplace` and `cf create-service`) and bound it to your application using `cf bind-service`.
* Scaled your application using `cf scale`.
* Observed the application resiliency capability of Cloud Foundry by killing an instance.
* Cleaned it all up.
