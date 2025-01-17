---
title: tiup dm reload
---

# tiup dm reload

After [modifying the cluster configuration](/tiup/tiup-component-dm-edit-config.md), the cluster needs to be reloaded using the `tiup dm reload` command for the configuration to take effect. This command publishes the configuration of the control machine to the remote machine where the service is running and restarts the service in order according to the upgrade process. The cluster remains available during the restart process.

## Syntax

```shell
tiup dm reload <cluster-name> [flags]
```

`<cluster-name>`: the name of the cluster to operate on.

## Options

### -N, --node

- Specifies the nodes to be restarted. If not specified, all nodes are restarted. The value of this option is a comma-separated list of node IDs. The node ID is the first column of the [cluster status](/tiup/tiup-component-dm-display.md) table.
- Data type: `strings`
- Default: `[]`, which means all nodes are selected.

> **Note:**
>
> + If the `-R, --role` option is specified at the same time, then the service status in their intersection is restarted.
> + If the `--skip-restart` option is specified, the `-N, --node` option is invalid.

### -R, --role

- Specifies the roles to be restarted. If not specified, all roles are restarted. The value of this option is a comma-separated list of node roles. The role is the second column of the [cluster status](/tiup/tiup-component-dm-display.md) table.
- Data type: `strings`
- Default: `[]`, which means all roles are selected.

> **Note:**
>
> + If the `-N, --node` option is specified at the same time, the services in their intersection is restarted.
> + If the `--skip-restart` option is specified, the `-R, --role` option is invalid.

### --skip-restart

The `tiup dm reload` command performs two operations:

- Refreshes all node configurations
- Restarts the specified node

After you specify the `--skip-restart` option, it only refreshes the configuration without restarting any nodes, so that the refreshed configuration is not applied and does not take effect until the next restart of the corresponding service.

- Data type: `BOOLEAN`
- Default: false

### -h, --help

- Prints the help information.
- Data type: `BOOLEAN`
- Default: false

## Output

The execution log of the tiup-dm.