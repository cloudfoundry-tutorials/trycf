+++
title = "Provisioning a Database"
weight = "7"
+++


Your app is now running, but it doesn't have a database. If you view your application in a browser, you will see the database is missing. Let's add a database.

*"But wait... I don't want to learn how to install, configure and manage MySQL, MariaDB, Postgres, etc."*

No problem. The Cloud Foundry marketplace is a collection of services that can be provisioned on demand. Your marketplace may differ depending on the Cloud Foundry distribution you are using.

* You can see the marketplace by running:

  ```sh
  cf marketplace
  ```

  Inside the marketplace, you will find database services (like MySQL or MariaDB) that you can provision on demand. Service information by provider is below.
  
* You can provision a new instance using `cf create-service`:

  ```sh
  cf create-service <SERVICE> <PLAN> first-push-db
  ```

  Let's dissect the above command:

  * The `<SERVICE>` is the name of the offering as listed in the marketplace (see below).
  * The `<PLAN`> is the tier or type of service to create (see below).
  * `first-push-db` is a descriptive name for this database instance as referred to in Cloud Foundry. Again, this name is used by humans, and can be whatever you want.

> NOTE: The application was built for training purposes only and does not store any actual data. Therefore, you can pick any database service from the marketplace. It does not have to be MySQL or MariaDB. We provide the service names by provider below solely to make it easier.

| Provider              | SERVICE      | PLAN               |
|-----------------------|--------------|--------------------|
| anynines              | a9s-mysql101 | mysql-single-small |
| cloud.gov             | aws-rds      | shared-mysql       |
| IBM Cloud             | mysql        | *varies*           |
| SAP Cloud Platform    | postgresql-db| trial              |
| SUSE                  | mariadb      | 10-1-34            |
| Swisscom              | mariadbent   | usage              |

> Many of the service offerings above contain multiple plans. When possible, we highlighted the smallest (often free) plan.

#### Checking Your Work

You should be able to see a new service instance using `cf services`:

```
Getting services in org cloudfoundry-training / space development as steve@example.com...
OK

name            service   plan    bound apps   last operation
first-push-db   mysql     free                create succeeded
```

> NOTE: You may also see the last operation marked as `create in progress`. This simply means the service instance is still being created. You can re-run `cf services` a few times until the instance has the `create succeeded` status.

### Okay, so what happened now?

Behind each service in the marketplace is a service broker (a broker can provide multiple services). Service brokers encapsulate the complexity of provisioning and interacting with different services using a standard API, the [Open Service Broker API](https://www.openservicebrokerapi.org/). The marketplace is populated when Cloud Foundry invokes the broker to find out what services it is offering. Those offerings include one or more plans which detail service levels or tiers of service. When you issued the `create-service` command, Cloud Foundry made a call to the broker to provision a database instance according to the plan.

*And what didn't happen?*

You didn't learn how to deploy, configure and manage the database. You didn't figure out service levels or routing. You simply used a standard API to provision a new instance.

Now that we have our instance, let's bind it to our app.
