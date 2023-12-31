# Chapter 3

## Page 33

Change the period between these sentences to a dash:

> ... and by looking at three of the most common resource types – packages, files, and services. You will see how to find out the attributes that are available to a resource and how to declare a state.

can be written as,

> ... and by looking at three of the most common resource types – packages, files, and services – you will see how to find out the attributes that are available to a resource and how to declare a state.

## Page 36

The class resource declaration has one typo:

* Line 2: `paramter1 => 'value1',` should instead be: `parameter1 => 'value1',`

:notebook: The bulleted list for the defined type declaration differs from the class declaration from the previous page. Suggestion: do not parenthetically identify the opening and closing elements.

Example:

* The `define` keyword
* The name of the defined type
* Parameters within ()
* Type definition code within {}

```puppet
define exampledefine (
  String user = "${title}",
  String group,
) {
  user { ${user}: }
  group { ${group}: }
  file { '/export/home/${user}/.examplesetting':
    user    => ${user},
    group   => ${group},
    content => "User is ${user} and group is ${group}",
  }
}
```

## Page 37

The sentence,

> This example has its dangers since if the second declaration for `user2` also used a group of `group1`, this would result in a duplicated resource declaration.

can be written to add emphasis the word 'also' to make it clear to the reader that this is a hypothetical situation and is not a comment on how the example code above it is written.

Example,

> This example has its dangers. If the declaration for `user2` ***also*** used `group1`, this would result in a duplicated resource declaration for `group1`.

In the sentence that ends,

> ... prioritizing conflict between resources.

'conflict' should be either 'conflicts' or 'a conflict'.

:notebook:

> Each resource will have a type ...

Can be written,

> Each resource has a type ...

## Page 38

As with the defined type introduction, the formatting could more closely match the class formatting:

* Open with the resource type, such as `file`, with no quotes and lowercase
* An open brace {
* The title of the resource in quotes
* A colon :
* A list of attribute name/value pairs separated with `=>` and ending with a comma ,
* A closing brace }

## Page 40

The code example has one typo:

* Line 7: `name   => "$apach_package_name",` should instead be `name   => $apache_package_name,`

:notebook: The example could be rewritten to use the `os.family` fact with 'Red Hat'. Updated formatting to match the Puppet style guide and stricter linting.

```puppet
$apache_package_name = $facts['os']['family']? {
  'Red Hat' => 'httpd',
  default   => 'apache2',
}
package { 'apache':
  ensure => latest,
  name   => $apache_package_name,
}
```

## Page 42

:notebook: The sentence,

> This sets several attributes to defaults, resulting in using the default provider for the underlying operating system, such as yum for Red Hat or, for Windows, the Windows provider ...

could be written,

> This sets several attributes to defaults, resulting in using the default provider for the underlying operating system, such as yum or dnf for Red Hat or the windows provider for Windows ...

## Page 43

The reference to `.bin` should instead be `.msi`.

:notebook: Red Hat Enterprise Linux 8+ and distributions based on RHEL 8 cannot install the `cowsay` package without first enabling EPEL.

## Page 44

The sentence,

> To create and enforce a resource, we must select the value of a file and use `direct` to create a directory or directory nest or `link` to create a symbolic link.

Contains one typo: `direct` should be `directory`. In addition, the term "directory nest" is uncommon and should be "nested directories."

The example `file` resource has incorrect spacing for the resource title, quotes the `ensure` value, and uses back slashes instead of forward slashes for the `path` value.

It should be formatted as:

```puppet
file { 'Puppet directory':
  ensure => directory,
  path   => 'C:/ProgramData/PuppetLabs',
}
```

## Page 45

The example `file` resource has hash rockets that are not aligned and the content had inconsistant spacing. It should be formatted as follows:

```puppet
file { 'Example config':
  ensure  => file,
  path    => '/app/exampleapp/config.txt',
  owner   => 'exampleapp',
  group   => 'examplegroup',
  content => "verbose = true\nselinux = permissive",
}
```

The statement,

> ... the comparative nature of Puppet, which uses `md5` checksums for content, ...

As of Puppet 7, the default digest algorithm is SHA256 [PUP-10583](https://www.puppet.com/docs/puppet/7/release_notes_puppet.html#enhancements_puppet_7-0-0-pup-10583).

## Page 46

The statement,

> The `purge` parameter can only be used with `ensure` set to `directory` or `recursive` set to `true` ...

Should read,

> The `purge` parameter can only be used with `ensure` set to `directory` or `recurse` set to `true` ...

Or follow the Puppet 8 documentation entry:

> [The `purge`] option only makes sense when `ensure => directory` and `recurse => true`.

The `recurse` example has incorrect spacing and `ensure => directory` does not need to be quoted. It should be formatted as follows:

```puppet
file { 'Remove apache config files outside of puppet control':
  ensure  => directory,
  purge   => true,
  recurse => true,
  path    => '/etc/httpd/conf',
}
```

The `target` example has incorrect spacing and is missing quotes for the `path` and `target` values. Capitalization for "Python" and "RHEL" added with formatting as follows:

```puppet
file { 'Picking a Python on RHEL 8':
  ensure => link,
  path   => '/usr/bin/python3',
  target => '/usr/bin/python',
}
```

The following is not a correction; however, the Puppet language style guide would format the `source` example thus,

```puppet
file { '/etc/exampleapp.conf':
  source => [
    "nfsserver:///exampleapp/conf.${host}",
    "nfsserver:///exampleapp/conf.${operatingsystem}",
    'nfsserver:///exampleapp/conf',
  ]
}
```

## Page 47

The statement,

> The replace parameter should be used sparingly, but if set to `true`, allows for a file to have content enforced only if it does not exist. If the file exists, the state is met. This can be useful for applications that require an initial configuration file but then overwrite it.

Should read,

> The replace parameter should be used sparingly, but if set to `false`, allows for a file to have content enforced only if it does not exist ...

From the [Puppet 8 documentation](https://www.puppet.com/docs/puppet/8/types/file.html#file-attribute-replace):

> **replace**
>
> Whether to replace a file or symlink that already exists on the local system but whose content doesn't match what the `source` or `content` attribute specifies.  Setting this to false allows file resources to initialize files without overwriting future changes. Note that this only affects content; Puppet will still manage ownership and permissions.

## Page 48

For the `service` example, the values for `enable` do not need to be quoted and should be formatted as follows:

```puppet
service { 'wuauserv':
  ensure       => running,
  enable       => delayed,
  logonaccount => 'LocalSystem',
}
service { 'bam':
  ensure => stopped,
  enable => false,
}
```

The statement,

> Comparing this to `systemd`, the default provider for RHEL 8 and other Linux systems, we can see in the description under supported features that `systemctl` does not have delayed login or `manual` but does have `mask`, which, in system terms, means it disables the service so not even services that are dependent on it can activate it.

Should read (correct 'in system terms' to 'in `systemd` terms'),

> Comparing this to `systemd`, the default provider for RHEL 8 and other Linux systems, we can see in the description under supported features that `systemctl` does not have delayed login or `manual` but does have `mask`, which, in `systemd` terms, means it disables the service so not even services that are dependent on it can activate it.

## Page 49

The formatting for the legacy service example should be:

```puppet
service { 'legacy service':
  ensure => running,
  enable => true,
  start  => '/opt/legacyapp/startlegacy -e production',
  stop   => '/opt/legacyapp/stoplegacy -e production',
  status => '/opt/legacyapp/legacystatus -e production',
}
```

## Page 50

There are two formatting corrections for the `metaparameters` code example. There is no comma after the package `name` attribute and the `service` resource is declared with a capitalized 'S' and lacks a space following the opening brace. It should be formatted as follows:

```puppet
package { 'example app package':
  ensure => latest,
  name   => 'exampleapp',
  before => File['example app configuration'],
}
file { 'example app configuration':
  content => 'attribute=value',
  notify  => Service['example app service'],
}
service { 'example app service':
  name    => 'exampleapp',
  enable  => true,
  ensure  => running,
  require => Package['example app package'],
}
```

The resource type dependency array example has two formatting corrections: there is an extra space in the resource title and no closing bracket for the array. In addition, the resource title or `path` attribute should use forward slashes as recommended in the [file resource documentation](https://www.puppet.com/docs/puppet/8/types/file.html#file-attribute-path) and should be formatted as:

```puppet
file { 'C:/Program Files/Common Files/Example':
  require => Package['package1', 'package2'],
}
```

## Page 51

In the statement,

> The code can also be run in **noop mode**,

'mode' does not need to be in bold face.

The `grafana.ini` code example uses upper case key names; however, the [Grafana documentation](https://grafana.com/docs/grafana/latest/setup-grafana/configure-grafana/) use only lower case key names and should be formatted as:

```ini
[server]
protocol = HTTP
http_port = 8080
```

## Page 52

There are a number of formatting errors in the closing paragraph under the sub heading "User and group types".

`<name of computer\<user name>`

Should be,

`<name of computer>\<user name>`

The code formatting for the statement,

> So, for example, `'DESKTOP-1MT10AJ\david`, `'BUILTIN\david'` and `david` are all treated
the same by Puppet.

Is inconsistent with missing single quotes for the first and third user names and should be formatted as:

> So, for example, `'DESKTOP-1MT10AJ\david'`, `'BUILTIN\david'` and `'david'` are all treated
the same by Puppet.

The Windows and Unix account and group code example contains a number of formatting errors and should be formatted as follows. I have reformatted the arrays so they are not on a single line and match the Puppet language style guide.

```puppet
user { 'david':
  ensure => present,
  groups => [
    'BUILTIN\Administrators',
    'BUILTIN\Users',
  ],
}
group { 'Users':
  ensure => present,
  members => [
    'NT AUTHORITY\INTERACTIVE',
    'NT AUTHORITY\Authenticated Users',
    'DESKTOP-1MT10AJ\david',
  ],
}
user { 'ubuntu':
  ensure             => present,
  comment            => 'Ubuntu',
  gid                => 1000,
  groups             => [
    'adm',
    'dialout',
    'cdrom',
    'floppy',
    'sudo',
    'audio',
    'dip',
    'video',
    'plugdev',
    'lxd',
    'netdev',
  ],
  home               => '/home/ubuntu',
  password           => '!',
  password_max_age   => 99999,
  password_min_age   => 0,
  password_warn_days => 7,
  shell              => '/bin/bash',
  uid                => 1000,
}
group { 'ubuntu':
  ensure => present,
  gid    => 1000,
}
```

## Page 53

:notebook: The statement,

> We can achieve this if the command itself is already idempotent, such as `apt-get update` ...

`apt-get update` is arguably *not* idempotent as the command updates a catalog file after every run and may exit with a non-zero status.

In the paragraph,

> In the first case, if the command is idempotent, it will do no harm, but it will log in each Puppet run that it has run, and therefore using the other two methods is better to avoid the exec reporting runs.

It should reference "the other three methods ..." (`onlyif`, `unless`, and `creates`). If the language of the paragraph is referring to the use of `onlyif` then it should make it clear that "the first case" is `onlyif`.

In the `exec` code example for disabling public Chocolatey access, the hash rockets do not align. Indentation for both `exec` examples differ (pages 53 and 54). One use four spaces, the other uses three.

## Page 54

There are too many spaces for the third `exec` code scenario. The example should be formatted as follows:

```puppet
exec { 'refresh exampleapp configuration':
  command     => '/bin/exampleapp/rereadconfig',
  refreshonly => true,
  subscribe   => File['config file'],
}
file { 'config file':
  path    => '/etc/exampleapp/configfile',
  content => 'setting 1 = value',
}
```

There is no Puppet version 7.9+ as referenced in the statement,

> On Unix platforms, a recent feature called parametrized execs was introduced with Puppet 6.24+ and 7.9+ ...

I have not yet identified which 7.2+ (presumably) release added parameterized `exec`.

The parameterized `exec` code example has a typo for 'parameterized', has too many spaces and does not include a colon after the resource title.

The example should be formatted as follows:

```puppet
exec { 'parameterized command':
  command => ['/bin/echo', 'real parameters; rm -rf /'],
}
```

## Page 56

The Augeas code example has too many spaces and the resource type should be lower case. It should be formatted as follows:

```puppet
augeas { 'remove John from access.conf':
  changes => 'rm /files/etc/security/access.conf/*[user="john"]',
}
```

:notebook: The `notify` code example should have a space prior to the closing brace, as follows,

```puppet
notify { 'print a message to logs': }
```

## Page 57

The `audit` code example has too many spaces and the resource title does not end with a colon. It should be formatted as follows:

```puppet
file { '/var/tmp/example':
  mode  => '0770',
  audit => [owner,group],
}
```

## Page 58

The example code for `tag` has too many spaces before the hash rockets, the value for `ensure` need not be quoted. It should be formatted as follows:

```puppet
class example::access {
  group { 'ubuntu':
    ensure => present,
    gid    => 1000,
    tag    => ['pci','sox'],
  }
  user { 'ubuntu':
    ensure => present,
    tag    => 'pci',
  }
}
```

The `resources` metatype code example does not follow the [Puppet language style guide](https://www.puppet.com/docs/puppet/8/style_guide.html#style_guide_module_design-spacing) for spacing the resource title. It should be formatted as follows:

```puppet
resources { 'user':
  purge => true,
  noop  => true,
}
```

## Page 59

Spacing in the array of titles code example is invalid and does not match the style guide. It should be formatted as follows:

```puppet
file { ['/opt/example1','/opt/example1/etc','/opt/example1/bin']:
  owner => 'user',
  group => 'user',
  mode  => '0750',
}
```

The overriding parameters code example has too many spaces before the hash rockets and no space between `File` and the overridden resource title. It should be formatted as follows:

```puppet
File ['/opt/example/bin/'] {
  group => 'other_group',
  audit => true,
}
```

## Page 60

Indentation for the example `case` statement for the splat attribute is inconsistent; there are too many spaces before the hash rockets; the splat attribute references a brace-enclosed variable when it should not; and the quoted strings should use single quotes instead of double quotes. It should be formatted as follows:

```puppet
case $facts['os']['name'] {
  /^(Debian|Ubuntu)$/: {
    $package_options = {
      'name' => 'apache2'
    }
  }
  default: {
    $package_options = {
      'name' => 'httpd'
    }
  }
}
package { 'http':
  ensure => latest,
  *      => $package_options,
}
```

The statement,

> This results in the package `http` resource using the name `http2` for Ubuntu and Debian systems ...

Should be,

> This results in the package `http` resource using the name `apache2` for Ubuntu and Debian systems ...

In the lab, the instruction,

> As a second exercise, create a separate manifest to create some users on the Linux client, `linux_users.pp create 3 users exampleappdev, exampleapptest, exampleappprod`, and a
group, `exampleapp`, with all the users using this group as their primary group.

Should be,

> As a second exercise, create a separate manifest to create some users on the Linux client, `linux_users.pp`. Create three users: `exampleappdev`, `exampleapptest`, and `exampleappprod`. Create the group `exampleapp` with all three users using this group as their primary group.

## Page 61

The code example for the abstract resource type references an undeclared variable, uses `resource` instead of `Resource`, and uses incorrect quoting that results in an unexpected end of file error.

It should be formatted as follows:

```puppet
$mytype = exec
Resource[$mytype] { '/bin/echo "don\'t use this" > /tmp/badidea':
  creates => '/tmp/badidea',
}
```

Likewise, the simple translation should be formatted as follows:

```puppet
exec { '/bin/echo "don\'t use this" > /tmp/badidea':
  creates => '/tmp/badidea',
}
```

## Page 62

:notebook: In the code example for the `default:` resource body, one array ends with a comma but the other does not.

The code example for the "Resource default syntax" uses a lower case 'f' for `file` instead of the upper case `File` as well as too many spaces before the hash rockets. The example should be formatted as follows:

```puppet
File {
  owner => 'exampleapp',
  group => 'exampleapp',
  mode  => '0660',
}
```

The `schedule` code examples also have too many spaces before or within the hash rockets and should be formatted as follows:

```puppet
schedule { 'Friday Night':
  day   => 'Friday',
  range => '18 - 9',
}
```

```puppet
exec { '/bin/echo weekend start > /tmp/example':
  schedule => 'Friday Night',
}
```

:notebook: The statement in the first paragraph under the "Exporters and collectors" has this statement,

> This is done by exporting the information to the PuppetDB database, which Puppet runs will consult with when collecting.

I would make the sentence more clear by adding 'resources' to the end of the sentence:

> This is done by exporting the information to the PuppetDB database, which Puppet runs will consult with when collecting resources.

## Page 63

:notebook: The statement,

> Exporting a resource just involves adding `@@` in front of a normal resource declaration.

Can be,

> Exporting a resource requires adding `@@` in front of a normal resource declaration.

The code example for exporting resources references a legacy fact and has too many spaces before the hash rockets. It should be formatted as follows:

```puppet
@@host { "Oracle database host entry ${trusted['hostname']}" :
  name => 'dbserver1',
  ip   => '192.168.0.6',
  tag  => 'oracle',
}
```

