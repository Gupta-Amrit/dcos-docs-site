---
layout: layout.pug
navigationTitle:  dcos help
title: dcos help
menuWeight: 3
excerpt:

enterprise: false
---

<!-- This source repo for this topic is https://github.com/dcos/dcos-docs -->


# Description
Display DC/OS CLI help information.

# Usage

```bash
dcos help <subcommand>
```

# Options

| Name, shorthand | Default | Description |
|---------|-------------|-------------|
| `--help, h`   |             |  Print usage. |
| `--info`   |             |  Print a short description of this subcommand. |
| `--version, v`   |             | Print version information. |
| `<subcommand>`   |             | The subcommand name. |

# Examples

## Display help for dcos config command

The `dcos help config` command is the same as `dcos config --help`.

```bash
dcos help config
Description:
    Manage the DC/OS configuration file.

Usage:
    dcos config --help
    dcos config --info
    dcos config set <name> <value>
    dcos config show [<name>]
    dcos config unset <name>
    dcos config validate

Commands:
    set
        Add or set a DC/OS configuration property.
    show
        Print the DC/OS configuration file contents.
    unset
        Remove a property from the configuration file.
    validate
        Validate changes to the configuration file.

Options:
    -h, --help
        Print usage.
    --info
        Print a short description of this subcommand.
    --version
        Print version information.

Positional Arguments:
    <name>
        The name of the property.
    <value>
        The value of the property.

Environment Variables:
    Configuration properties all have corresponding environment variables. If a
    property is in the "core" section (ex. "core.foo"), it corresponds to
    environment variable DCOS_FOO. All other properties (ex "foo.bar")
    correspond to enviroment variable DCOS_FOO_BAR.

    Environment variables take precendence over corresponding configuration
    property.
```
