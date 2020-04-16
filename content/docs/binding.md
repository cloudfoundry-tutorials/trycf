+++
title = "Binding a Database"
weight = "8"
+++

Now that you have a database instance, you need to tell your application about the instance so the app can use it. In Open Service Broker API terms this is called `binding`.

* Bind the service instance you created to your application:

  ```sh
  cf bind-service first-push first-push-db
  ```

* Now restart your application so that it picks up the change:

  ```sh
  cf restart first-push
  ```

#### Checking Your Work

If you re-run `cf services` you should see your app now bound to your database.

```
Getting services in org cloudfoundry-training / space development as steve@example.com...
OK

name            service   plan    bound apps   last operation
first-push-db   mysql     free   first-push   create succeeded
```

You can also refresh your app in the browser and should see it is now using the database (your service name and plan may vary).

### Okay, what happened?

When you issued the `bind-service` command, Cloud Foundry again made a call to a service broker. This time, the broker created credentials for your application and granted the necessary permissions to access the database. These credentials were returned to Cloud Foundry, which passed them to your application through an environment variable. This is why you needed to restart the app - so that it would pick up the new environment variable values containing the credentials. At this point, the app connects to the database using the credentials. The broker is not involved in this communication and your app treats it like any other database.

*And what didn't happen?*

You didn't learn to create new database users, set credentials and grant access to resources. You also didn't change any configuration files in the application since it is written to read config from the environment (the number III [12 factor](https://12factor.net/config) app best practice). You simply issued a single command and restarted the app.

Great! Now that the app is using an external database, let's scale it.
