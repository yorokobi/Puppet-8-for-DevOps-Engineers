# Chapter 6

## Page 130

The hash rockets for first code example under "Relationships and ordering" do not align for the `file` resource.

---

## Page 132

The multiple dependency code example is missing a closing quote for the `File[]` array and should employ line breaks for readability.

It should be formatted,

```puppet
package { 'exampleapp':
  ensure => latest,
  before => [
    File[
      '/opt/exampleapp.content',
      '/var/exampleapp.variables',
    ],
    Service['exampleapp', 'exampleapp2',]
  ]
}
```

---

## Page 133

In the second pararaph, the sentence,

> Of the built-in Puppet types, `service` `exec` and `package` can be refreshed.

Needs a comma between `service` and `exec`.

---

The hash rockets in the code example for the `service` resource do not align.

---

## Page 135

:notebook: The code examples for relationship arrows and containment should use three distinct `include` lines, one per class, rather than all three separated by commas on a single line.

---

## Page 137

The code example for `examplemodule::class3` has one too many single quotes: `attribute => 'value1''`. It should be `attribute => 'value1',`.

---

## Page 141

The node scope code example is missing the `$` prefix for the `$test` variable in the `example` class and the `notify` resources reference a non-existent `$testing` variable. Adding spaces before and after the `=` symbol aids in readability.

It should be formatted,

```puppet
$top = 'toptest'
$test = 'testing123'
notify "Top = ${top} node = ${node} local = ${local} test = ${test}"
notify "Access directly ${example::local}"
node default {
  include example
  $test = 'hello world'
  $node = 'nodetest'
  notify "Top = ${top} node = ${node} local = ${local} test = ${test}"
  notify "Access directly ${example::local}"
}
class example {
  $test = 'an example'
  $local = 'localtest'
  notify "Top = ${top} node = ${node} local = ${local} test = ${test}"
}
```

---

The reference to `testing` in the sentence,

> The first `notify` would fail to find the local or node variable since it is in the global scope, and `testing` would be set to `testing123`.

Should be,

> The first `notify` fails to find the `$local` or `$node` variables as they are in the global scope, and `$test` is set to `testing123`.

---

## Page 143

:notebook: The sentence,

> This allows for these resources to be restarted, reinstalled, or rerun when necessary, such as when a configuration file changes.

Should be,

> This allows for these resources to rerun, reinstall, or restart when necessary, such as when a configuration file changes.

To match the "`exec`, `package`, and `service`" resources in the sentence immediately preceding it.

---

:notebook: The sentence,

> Additionally, we acknowledged that although resources should be assumed to have no order, they are in fact applied in the order they are written in a manifest to ensure consistency across environments.

If resources are applied in the order they are written, why mention that they "should be assumed to have no order"? Acknowledging that certain versions of Puppet applied resources in any order at that point in the chapter is sufficient.
