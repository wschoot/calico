---
title: calicoctl create
redirect_from: latest/reference/calicoctl/create
canonical_url: 'https://docs.projectcalico.org/v3.7/reference/calicoctl/commands/create'
---

This sections describes the `calicoctl create` command.

Read the [calicoctl command line interface user reference]({{site.baseurl}}/{{page.version}}/reference/calicoctl/)
for a full list of calicoctl commands.

> **Note**: The available actions for a specific resource type may be
> limited based on the datastore used for {{site.prodname}} (etcdv3 / Kubernetes API).
> Please refer to the
> [Resources section]({{site.baseurl}}/{{page.version}}/reference/resources/)
> for details about each resource type.
{: .alert .alert-info}


## Displaying the help text for 'calicoctl create' command

Run `calicoctl create --help` to display the following help menu for the
command.

```
Usage:
  calicoctl create --filename=<FILENAME> [--skip-exists] [--config=<CONFIG>] [--namespace=<NS>]

Examples:
  # Create a policy using the data in policy.yaml.
  calicoctl create -f ./policy.yaml

  # Create a policy based on the JSON passed into stdin.
  cat policy.json | calicoctl create -f -

Options:
  -h --help                 Show this screen.
  -f --filename=<FILENAME>  Filename to use to create the resource.  If set to
                            "-" loads from stdin.
     --skip-exists          Skip over and treat as successful any attempts to
                            create an entry that already exists.
  -c --config=<CONFIG>      Path to the file containing connection
                            configuration in YAML or JSON format.
                            [default: /etc/calico/calicoctl.cfg]
  -n --namespace=<NS>       Namespace of the resource.
                            Only applicable to NetworkPolicy, NetworkSet, and WorkloadEndpoint.
                            Uses the default namespace if not specified.

Description:
  The create command is used to create a set of resources by filename or stdin.
  JSON and YAML formats are accepted.

  Valid resource types are:

    * bgpConfiguration
    * bgpPeer
    * felixConfiguration
    * globalNetworkPolicy
    * hostEndpoint
    * ipPool
    * networkPolicy
    * networkSet
    * node
    * profile
    * workloadEndpoint

  Attempting to create a resource that already exists is treated as a
  terminating error unless the --skip-exists flag is set.  If this flag is set,
  resources that already exist are skipped.

  The output of the command indicates how many resources were successfully
  created, and the error reason if an error occurred.  If the --skip-exists
  flag is set then skipped resources are included in the success count.

  The resources are created in the order they are specified.  In the event of a
  failure creating a specific resource it is possible to work out which
  resource failed based on the number of resources successfully created.
```
{: .no-select-button}

### Examples

1. Create a set of resources (of mixed type) using the data in resources.yaml.

   ```bash
   calicoctl create -f ./resources.yaml
   ```

   Results indicate that 8 resources were successfully created.

   ```bash
   Successfully created 8 resource(s)
   ```
   {: .no-select-button}

1. Create the same set of resources reading from stdin.

   ```bash
   cat resources.yaml | calicoctl apply -f -
   ```

   Results indicate failure because the first resource (in this case a Profile)
   already exists.

   ```bash
   Failed to create any resources: resource already exists: Profile(name=profile1)
   ```
   {: .no-select-button}

### Options

```
-f --filename=<FILENAME>  Filename to use to create the resource.  If set to
                          "-" loads from stdin.
   --skip-exists          Skip over and treat as successful any attempts to
                          create an entry that already exists.
-n --namespace=<NS>       Namespace of the resource.
                          Only applicable to NetworkPolicy and WorkloadEndpoint.
                          Uses the default namespace if not specified.
```
{: .no-select-button}

### General options

```
-c --config=<CONFIG>      Path to the file containing connection
                          configuration in YAML or JSON format.
                          [default: /etc/calico/calicoctl.cfg]
```
{: .no-select-button}

## See also

-  [Installing calicoctl]({{site.baseurl}}/{{page.version}}/getting-started/calicoctl/install)
-  [Resources]({{site.baseurl}}/{{page.version}}/reference/resources/) for details on all valid resources, including file format
   and schema
-  [NetworkPolicy]({{site.baseurl}}/{{page.version}}/reference/resources/networkpolicy) for details on the {{site.prodname}} selector-based policy model
