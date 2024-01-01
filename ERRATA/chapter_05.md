# Chapter 5

## Page 99

:notebook: In the sentence,

> When Puppet is run, either via the agent or by running `puppet apply` on the command line, Facter will run, with legacy facts, disabled in Puppet 8 or enabled in Puppet 7 and below and the output will be assigned to global variables.

The two commas surrounding "with legacy facts" are not necessary or should follow "Puppet 8". A comma after "and below" makes more sense.

> When Puppet is run, either via the agent or by running `puppet apply` on the command line, Facter will run with legacy facts disabled in Puppet 8 or enabled in Puppet 7 and below, and the output will be assigned to global variables.

:notebook: The reference to the `$facts` array in this sentence,

> These variables can then be accessed in Puppet manifests in two ways – either directly by the name of the fact on a global variable or via the facts array.

May instead be formatted (and passive voice removed):

> These variables are accessed in Puppet manifests in two ways – either directly by the name of the fact on a global variable or via the `$facts` array.

The sentence,

> For example, in the following code, the notify resources would access the `kernel` and `os family` variables and print logging messages containing the kernel and os families of the host it was run on:

Refers to the `os.family` fact as `os family` and calls them variables instead of facts. It should be,

> For example, in the following code, the notify resources would access the `kernel` and `os.family` facts and print logging messages containing the kernel and os family of the host it was run on:

The subsequent code example does not properly refer to elements of the `$facts` hash, lacking the single quoted hash keys as well as the closing brace for the `os.family` fact reference. It should be formatted:

```puppet
notify { "This client's kernel is ${facts['kernel']}": }
notify { "This client is a member of the os family ${facts['os']['family']}": }
```

## Page 100

The indentation for the example `factor.conf` is inconsistent.

## Page 101

:notebook: In the sentence,

> The cli section sets a log level with a string of (`none`, `trace`, `debug`, `info`, `warn`, `error`, `fatal`) and has three options: `verbose`, `trace`, and `debug`. Each of these three options is enabled or disabled with a `true` or `false` Boolean.

The list of logging levels does not need parentheses and the paragraph can be simplified thus,

> The CLI section sets the log level with a value of `none`, `trace`, `debug`, `info`, `warn`, `error`, or `fatal` and has three Boolean options: `verbose`, `trace`, or `debug`, which are enabled or disabled with either `true` or `false`.

## Page 102

The conclusion of the note at the top of the page does not need the word "basis."

The sentence,

> In Chapter 8, you will learn how external facts can be distributed to clients from modules via the plugin sync process, where facts are added from modules contained in a `facts.d` folder within the module.

Can be simplified by removing ", where facts are added from modules contained."

## Page 103

In the note,

> Puppet can be run as a non-root user on UNIX-based systems, while external facts can be stored in `~/.facter/facts.d/` ...

The use of "while" should be "with." For example, with passive voice removed:

> Puppet can run as a non-root user on UNIX-based systems with external facts stored in `~/.facter/facts.d/`.

The YAML-formatted external facts example does not pass `yamllint` due to too many spaces before and, in the case of `Application`, after the colons. It should be formatted:

```yaml
---
Application: exampleapp
Use: Production
Owner: exampleorg
...
```

:notebook: The JSON-formatted external facts is easier to read when formatted as:

```json
{
  "Application": "exampleapp",
  "Use": "Production",
  "Owner": "exampleorg"
}
```

:notebook: The paragraph about Windows line endings could be a Note section and "BOM" should be "byte order mark (BOM)."

The YAML-formatted structured fact example has the same problem as the simpler external facts example: too many spaces before (and after) the colons. In addition, as formatted the keys `Use` and `Owner` are duplicated, the `Owner` array does not have a colon and its elements are not properly indented.

In order for the `facter` commands on page 104 to work, it should be formatted as:

```yaml
---
application:
  exampleapp:
    use: Production
    owner:
      - exampleorg
      - anotherorg
  anotherapp:
    use: Production
    owner: exampleorg
...
```

## Page 104

In the Bash shell example, the system calls to `pidof` and `ps` need to be surrounded by parentheses, not braces. In addition, the `ps -C` command does not return the percent CPU or memory used.

```bash
#!/bin/bash
echo "exampleapp_pid = $(pidof exampleapp)"
echo "exampleapp_cpu_use = $(ps -C exampleapp) %cpu"
echo "exampleapp_memory_use = $(ps -C exampleapp) %mem"
```
