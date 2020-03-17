+++
title = "Installing the CLI"
weight = "4"
+++

The CLI, or Command Line Interface, is the tool you will use to interact with Cloud Foundry. The CLI runs in a terminal window on your computer and makes REST calls to the Cloud Foundry API.

* Follow the instructions to install the CLI: [https://github.com/cloudfoundry/cli#downloads](https://github.com/cloudfoundry/cli#downloads)

* You can test that it works by running `cf version`:

  ```sh
  cf version
  ```

  And you will see output similar to:

  ```
  cf version 6.43.0+815ea2f3d.2019-02-20
  ```

The CLI is a self-documenting tool. For example, you can run:

* `cf help` to see a list of the most commonly used commands
* `cf help -a` to see a list of all the available commands
* `cf <command> --help` to see details on using a specific command

Once you have the CLI installed and working, it is time to login to Cloud Foundry.
