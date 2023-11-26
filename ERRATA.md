# Errata

Entries with :notebook: are my opinion.

#### Page 6

The code example has two typos:

* Line 1: `user { 'david'` should instead be `user { 'david':`
* Line 2: `uid => '123'` should instead be `uid => '123',`

#### Pages 7-8

The code example should be as follows:

```puppet
user { 'exampleapp':
  uid => '1234',
  gid => '123',
}
group { 'exampleapp':
  gid => '123',
}
file { '/opt/exampleapp/':
  ensure => directory,
  owner  => 'exampleapp',
  group  => 'exampleapp',
  mode   => '0755',
}
file { '/etc/exampleapp/':
  ensure => directory,
  owner  => 'exampleapp',
  group  => 'exampleapp',
  mode   => '0750',
}
```

#### Page 10

The sentence ending,

> ... modules provide sharable and reusable single-use technical installations.

should probably read,

> ... modules provide sharable and reusable single-use technical implementations.

#### Page 11

The code examples have one typo each:

`profile::os_security:email_enabled: true` should instead be: `profile::os_security::email_enabled: true`

`profile::exampleapp:uid: '1235'` should instead be: `profile::exampleapp::uid: '1235'`

:notebook: Reader's comment for page 45:

The sentence,

> One of the most important points of creating these patterns is to avoid hardcoded values in your modules.

conflicts somewhat with the sentence from chapter 9,

> The first key thing is if the data doesn't vary over nodes and it's only used once, the simplest thing is to hardcode the data in Puppet code ...

#### Page 15

The code example has two typos:

* Line 2 `:git => 'https://github.com/exampleorg/exampleapp'` should instead be `:git => 'https://github.com/exampleorg/exampleapp.git',`

:notebook: Reader's comment for page 50:

The sentence,

> Normally, this means a minimum of a development environment and a production environment. So, changes can be tested against servers in development, and then successfully tested ones can be deployed to production.

should instead be,

> Normally, this means a minimum of a development environment and a production environment so changes can be tested against servers in development and then successfully tested ones can be deployed to production.

:notebook: Reader's comment for page 53:

The reference to the latest version of Puppet should be changed from 7 to 8. All installation URIs appear to use Puppet 8 even though the Azure lab installs Puppet 7.

#### Page 20

The bullet point:

* A Linux environment using package managers such as apt for Ubuntu or RHEL-based using Yum.

Should instead be:

* A Linux environment using package managers such as apt/apt-get for Debian based distributions or yum/dnf for Red Hat based distributions.

The final bullet point for Visual Studio Code extensions references an application unrelated to VSCode: `pecdm`. The bullet point should be shifted left to align with "The GitHub CLI" etc.

#### Page 24

"Augeas" is misspelled in the sentence:

> "Augeuas is very advanced but often over-complicated ..."

The URL <https://validate.puppet.com/> is not valid. No such website exists. This is referenced on pages 24, 40, 131, and 143.

:notebook: Reader's comments for pages 24-25:

The ending of the following sentence lacks a proper subject for what to develop and what to integrate with:

> One of the greatest issues with early Puppet development was the lack of a consensus around how to develop and a lack of integration.

The sentence,

> This is certainly not the only way to develop Puppet code, and your organization might require the usage of different tools deponding on the environment.

can be written,

> This is certainly not the only way to develop Puppet code and your organization might require using different tools, depending on the environment.

The claim that PDK will be covered "in full" in chapter 8 is misleading as PDK is not covered "in full" in that chapter.

Vim is referenced twice, once as 'Vim' and, in the same sentence, as 'VIM.' 'Vim' is correct as it is not an acronym.

The sentence ending,

> ... to avoid paying for unecessary virtual machine running time costs on Azure.

can be simplified (and the typo "unecessary" corrected) to,

> ... to avoid paying for unnecessary virtual machine time on Azure.

:notebook: Reader's comment for page 26:

References to 'Yum' or 'yum' should be replaced with 'dnf' as Red Hat Enterprise Linux 8+ (and related distributions) use 'dnf' by default. This is also true of the package provider for these distributions.

#### Page 29

The code example has one typo:

* Line 1: `mkdir ~workspace/pecdm` should instead be `mkdir -p ~workspace/pecdm`

:notebook: Reader's comment for page 29:

`~workspace` should be `~/workspace`. Example: `mkdir -p ~/workspace/pecdm`

#### Page 31

This sentence needs a space after the first comma:

> Puppet has its own learning site (<https://training.puppet.com/learn>),this ...

It should be:

> Puppet has its own learning site (<https://training.puppet.com/learn>), this ...

The sentence,

> Puppet's support knowledge base was made public in April 2022, ...

should be a new paragraph.

The sentence,

> Puppet previously run two, ... which had to be paid for and lasted 3 ...

Should instead be,

> Puppet previously ran two, ... which had to be paid for and lasted three ...

In the paragraph that begins, "The key difference is that" the two words "self paced" should be hyphenated as "self-paced"

:notebook: Reader's comment for page 32:

The paragraph beginning,

> This section is not supposed to be an exhaustive ...

Can be simplified to,

> This section is not an exhaustive ...

#### Page 33

Change the period between these sentences to a dash:

> ... and by looking at three of the most common resource types – packages, files, and services. You will see how to find out the attributes that are available to a resource and how to declare a state.

can be written as,

> ... and by looking at three of the most common resource types – packages, files, and services – you will see how to find out the attributes that are available to a resource and how to declare a state.

#### Page 36

The class resource declaration has one typo:

* Line 2: `paramter1 => 'value1',` should instead be: `parameter1 => 'value1',`

:notebook: Reader's comment for page 36:

The bulleted list for the defined type declaration differs from the class declaration from the previous page. Suggestion: do not parenthetically identify the opening and closing elements.

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

#### Page 37

The sentence,

> This example has its dangers since if the second declaration for `user2` also used a group of `group1`, this would result in a duplicated resource declaration.

can be written to add emphasis the word 'also' to make it clear to the reader that this is a hypothetical situation and is not a comment on how the example code above it is written.

Example,

> This example has its dangers. If the declaration for `user2` ___also___ used `group1`, this would result in a duplicated resource declaration for `group1`.

In the sentence that ends,

> ... prioritizing conflict between resources.

'conflict' should be either 'conflicts' or 'a conflict'.

:notebook: Reader's comment for page 37:

> Each resource will have a type ...

Can be written,

> Each resource has a type ...

#### Page 38

As with the defined type introduction, the formatting could more closely match the class formatting:

* Open with the resource type, such as `file`, with no quotes and lowercase
* An open brace {
* The title of the resource in quotes
* A colon :
* A list of attribute name/value pairs separated with `=>` and ending with a comma ,
* A closing brace }

#### Page 40

The code example has one typo:

* Line 7: `name   => "$apach_package_name",` should instead be `name   => $apache_package_name,`

:notebook: Reader's comment for page 40:

The example could be rewritten to use the `os.family` fact with 'Red Hat'. Updated formatting to match the Puppet style guide and stricter linting.

```puppet
$apache_package_name = $facts['os']['family']? {
  'Red Hat' => 'httpd',
  default   => 'apache2',
}
package { 'apache':
  ensure => latest,
  name   => $apache_package_name,
}
```

#### Page 42

:notebook: Reader's comment for page 42:

The sentence,

> This sets several attributes to defaults, resulting in using the default provider for the underlying operating system, such as yum for Red Hat or, for Windows, the Windows provider ...

could be written,

> This sets several attributes to defaults, resulting in using the default provider for the underlying operating system, such as yum or dnf for Red Hat or the windows provider for Windows ...

#### Page 43

The reference to `.bin` should instead be `.msi`.

:notebook: Reader's comment for page 43:

Red Hat Enterprise Linux 8 and distributions based on RHEL 8 cannot install the `cowsay` package without first enabling EPEL.

#### Page 44

The sentence,

> To create and enforce a resource, we must select the value of a file and use `direct` to create a directory or directory nest or `link` to create a symbolic link.

Contains one typo. `direct` should be `directory`. In addition, the term "directory nest" is uncommon and should be "nested directories".

:notebook: Reader's comment for page 44:

```puppet
file {'Puppet directory' :
  ensure => 'directory',
  path   => 'C:\ProgramData\PuppetLabs',
}
```

To meet the style guide:

```puppet
file { 'Puppet directory':
  ensure => directory,
  path   => 'C:\ProgramData\PuppetLabs',
}
```

#### Page 45

The example `file` resource has hash rockets that are not aligned and the content had inconsistant spacing.

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

#### Page 46

The statement,

> The **purge** parameter can only be used with **ensure** set to **directory** or **recursive** set to **true** ...

Should read,

> The **purge** parameter can only be used with **ensure** set to **directory** or **recurse** set to **true** ...

Or follow the Puppet 8 documentation entry:

> [The `purge`] option only makes sense when `ensure => directory` and `recurse => true`.

The `recurse` example has incorrect spacing and `ensure => directory` does not need to be quoted. It should be formatted as follows:

```puppet
file { 'Remove apache config files outside of puppet control':
  ensure  => directory,
  purge   => true,
  recurse => true,
  path    => '/etc/httpd/conf',
}
```

The `target` example has incorrect spacing and is missing quotes for the `path` and `target` values. Capitalization for "Python" and "RHEL" added with formatting as follows:

```puppet
file { 'Picking a Python on RHEL 8':
  ensure  => link,
  path    => '/usr/bin/python3',
  target  => '/usr/bin/python',
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

#### Page 47

The statement,

> The replace parameter should be used sparingly, but if set to **true**, allows for a file to have content enforced only if it does not exist. If the file exists, the state is met. This can be useful for applications that require an initial configuration file but then overwrite it.

Should read,

> The replace parameter should be used sparingly, but if set to **false**, allows for a file to have content enforced only if it does not exist ...

From the [Puppet 8 documentation](https://www.puppet.com/docs/puppet/8/types/file.html#file-attribute-replace):

> **replace**
>
> Whether to replace a file or symlink that already exists on the local system but whose content doesn't match what the `source` or `content` attribute specifies.  Setting this to false allows file resources to initialize files without overwriting future changes.  Note that this only affects content; Puppet will still manage ownership and permissions.

#### Page 48

For the `service` example, the values for `enable` do not need to be quoted and should be formatted as follows:

```puppet
service { 'wuauserv':
  ensure       => running,
  enable       => delayed,
  logonaccount => 'LocalSystem',
}
service { 'bam':
  ensure => stopped,
  enable => false,
}
```

The statement,

> Comparing this to `systemd`, the default provider for RHEL 8 and other Linux systems, we can see in the description under supported features that `systemctl` does not have delayed login or `manual` but does have `mask`, which, in system terms, means it disables the service so not even services that are dependent on it can activate it.

Should read (correct 'system' to '`systemd`'),

> Comparing this to `systemd`, the default provider for RHEL 8 and other Linux systems, we can see in the description under supported features that `systemctl` does not have delayed login or `manual` but does have `mask`, which, in `systemd` terms, means it disables the service so not even services that are dependent on it can activate it.

#### Page 49

The formatting for the legacy service example should be,

```puppet
service { 'legacy service':
  ensure  => running,
  enable  => true,
  start   => '/opt/legacyapp/startlegacy -e production',
  stop    => '/opt/legacyapp/stoplegacy -e production',
  status  => '/opt/legacyapp/legacystatus -e production',
}
```

#### Page 50

There are two formatting corrections for the `metaparameters` code example. There is no comma after the package `name` attribute and the `service` resource is declared with a capitalized 'S' and lacks a space following the opening brace. It should be formatted as follows:

```puppet
package { 'example app package':
  ensure => latest,
  name   => 'exampleapp',
  before => File['example app configuration'],
}
file { 'example app configuration':
  content => 'attribute=value',
  notify  => Service['example app service'],
}
service { 'example app service':
  name    => 'exampleapp',
  enable  => true,
  ensure  => running,
  require => Package['example app package'],
}
```

The resource type dependency array example has two formatting corrections: there is an extra space in the resource title and no closing bracket for the array. In addition, the resource title or `path` attribute should use forward slashes as recommended in the [file resource documentation](https://www.puppet.com/docs/puppet/8/types/file.html#file-attribute-path) and should be formatted as:

```puppet
file { 'C:/Program Files/Common Files/Example':
  require => Package['package1', 'package2'],
}
```

#### Page 51

In the statement,

> The code can also be run in **noop mode**,

'mode' does not need to be in bold face.

The `grafana.ini` code example uses upper case key names; however, the [Grafana documentation](https://grafana.com/docs/grafana/latest/setup-grafana/configure-grafana/) use only lower case key names and should be formatted as:

```ini
[server]
protocol = HTTP
http_port = 8080
```

#### Page 52

There are a number of formatting errors in the closing paragraph under the sub heading "User and group types".

> <name of computer\<user name>

Should be,

> <name of computer>\<user name>

The code formatting for the statement,

> So, for example, `'DESKTOP-1MT10AJ\david`, `'BUILTIN\david'` and `david` are all treated
the same by Puppet.

Is inconsistent with missing single quotes for the first and third user names and should be formatted as: 

> So, for example, `'DESKTOP-1MT10AJ\david'`, `'BUILTIN\david'` and `'david'` are all treated
the same by Puppet.

The Windows and Unix account and group code example contains a number of formatting errors and should be formatted as follows. I have reformatted the arrays so they are not on a single line and match the Puppet language style guide.

```puppet
user { 'david':
  ensure => present,
  groups => [
    'BUILTIN\Administrators',
    'BUILTIN\Users',
  ],
}
group { 'Users':
  ensure  => present,
  members => [
    'NT AUTHORITY\INTERACTIVE',
    'NT AUTHORITY\Authenticated Users',
    'DESKTOP-1MT10AJ\david',
  ],
}
user { 'ubuntu':
  ensure             => present,
  comment            => 'Ubuntu',
  gid                => 1000,
  groups             => [
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
  home               => '/home/ubuntu',
  password           => '!',
  password_max_age   => 99999,
  password_min_age   => 0,
  password_warn_days => 7,
  shell              => '/bin/bash',
  uid                => 1000,
}
group { 'ubuntu':
  ensure => present,
  gid    => 1000,
}
```

#### Page 53

The statement,

> We can achieve this if the command itself is already idempotent,
such as `apt-get update` ...

`apt-get update` is arguably *not* idempotent as the command updates a catalog file after every run and may exit with a non-zero status.

In the paragraph,

> In the first case, if the command is idempotent, it will do no harm, but it will log in each Puppet run that it has run, and therefore using the other two methods is better to avoid the exec reporting runs.

It should reference "the other three methods ..." (`onlyif`, `unless`, and `creates`). If the language of the paragraph is referring to the use of `onlyif` then it should make it clear that "the first case" is `onlyif`.

In the `exec` code example for disabling public Chocolatey access, the hash rockets do not align. Indentation for both `exec` examples differ (pages 53 and 54). One use four spaces, the other uses three.

#### Page 54

There are too many spaces for the third `exec` code scenario. The exmaple should be formatted as follows:

```puppet
exec { 'refresh exampleapp configuration':
  command     => '/bin/exampleapp/rereadconfig',
  refreshonly => true,
  subscribe   => File['config file'],
}
file { 'config file':
  path    => '/etc/exampleapp/configfile',
  content => 'setting 1 = value',
}
```

There is no Puppet version 7.9+ as referenced in the statement,

> On Unix platforms, a recent feature called parametrized execs was introduced with Puppet 6.24+ and 7.9+ ...

I have not yet identified which 7.2+ (presumably) release added parameterized `exec`.

The parameterized `exec` code example has too many spaces and does not include a colon after the resource title.

The example should be formatted as follows:

```puppet
exec { 'parametrized command':
  command => ['/bin/echo', 'real parameters; rm -rf /'],
}
```

#### Page 56

The Augeas code example has too many spaces and the resource type should be lower case. It should be formatted as follows:

```puppet
augeas { 'remove John from access.conf':
  changes => 'rm /files/etc/security/access.conf/*[user="john"]',
}
```

The `notify` code example should have a space prior to the closing brace, as follows:

```puppet
notify { 'print a message to logs': }
```