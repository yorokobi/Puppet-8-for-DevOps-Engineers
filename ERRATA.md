# Errata

Entries with :notebook: are my opinion.

## Entire book

There are many references to `=>` but it is not called a 'hash rocket' until page 161. Given that 'hash rocket' is a common term for this combination of symbols, the use of the name should be used much earlier.

### Chapter 1

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

:notebook: The sentence,

> One of the most important points of creating these patterns is to avoid hardcoded values in your modules.

conflicts somewhat with the sentence from chapter 9,

> The first key thing is if the data doesn't vary over nodes and it's only used once, the simplest thing is to hardcode the data in Puppet code ...

#### Page 15

The code example has two typos:

* Line 2 `:git => 'https://github.com/exampleorg/exampleapp'` should instead be `:git => 'https://github.com/exampleorg/exampleapp.git',`

:notebook: The sentence,

> Normally, this means a minimum of a development environment and a production environment. So, changes can be tested against servers in development, and then successfully tested ones can be deployed to production.

should instead be,

> Normally, this means a minimum of a development environment and a production environment so changes can be tested against servers in development and then successfully tested ones can be deployed to production.

:notebook: The reference to the latest version of Puppet should be changed from 7 to 8. All installation URIs appear to use Puppet 8 even though the Azure lab installs Puppet 7.

### Chapter 2

#### Page 20

The bullet point:

* A Linux environment using package managers such as apt for Ubuntu or RHEL-based using Yum.

Should instead be:

* A Linux environment using package managers such as apt/apt-get for Debian based distributions or yum/dnf for Red Hat based distributions.

The final bullet point for Visual Studio Code extensions references an application unrelated to VSCode: `pecdm`. The bullet point should be shifted left to align with "The GitHub CLI" etc.

#### Page 24

"Augeas" is misspelled in the sentence:

> "Augeuas is very advanced but often over-complicated ..."

:notebook: (pages 24-25) The ending of the following sentence lacks a proper subject for what to develop and what to integrate with,

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

:notebook: References to 'Yum' or 'yum' should be replaced with 'dnf' as Red Hat Enterprise Linux 8+ (and related distributions) use 'dnf' by default. This is also true of the package provider for these distributions.

#### Page 29

The code example has one typo:

* Line 1: `mkdir ~workspace/pecdm` should instead be `mkdir -p ~workspace/pecdm`

:notebook: `~workspace` should be `~/workspace`. Example: `mkdir -p ~/workspace/pecdm`

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

:notebook: The paragraph beginning,

> This section is not supposed to be an exhaustive ...

Can be simplified to,

> This section is not an exhaustive ...

### Chapter

#### Page 33

Change the period between these sentences to a dash:

> ... and by looking at three of the most common resource types – packages, files, and services. You will see how to find out the attributes that are available to a resource and how to declare a state.

can be written as,

> ... and by looking at three of the most common resource types – packages, files, and services – you will see how to find out the attributes that are available to a resource and how to declare a state.

#### Page 36

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

#### Page 37

The sentence,

> This example has its dangers since if the second declaration for `user2` also used a group of `group1`, this would result in a duplicated resource declaration.

can be written to add emphasis the word 'also' to make it clear to the reader that this is a hypothetical situation and is not a comment on how the example code above it is written.

Example,

> This example has its dangers. If the declaration for `user2` ___also___ used `group1`, this would result in a duplicated resource declaration for `group1`.

In the sentence that ends,

> ... prioritizing conflict between resources.

'conflict' should be either 'conflicts' or 'a conflict'.

:notebook:

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

:notebook: The example could be rewritten to use the `os.family` fact with 'Red Hat'. Updated formatting to match the Puppet style guide and stricter linting.

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

:notebook: The sentence,

> This sets several attributes to defaults, resulting in using the default provider for the underlying operating system, such as yum for Red Hat or, for Windows, the Windows provider ...

could be written,

> This sets several attributes to defaults, resulting in using the default provider for the underlying operating system, such as yum or dnf for Red Hat or the windows provider for Windows ...

#### Page 43

The reference to `.bin` should instead be `.msi`.

:notebook: Red Hat Enterprise Linux 8+ and distributions based on RHEL 8 cannot install the `cowsay` package without first enabling EPEL.

#### Page 44

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

#### Page 45

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

#### Page 46

The statement,

> The `purge` parameter can only be used with `ensure` set to `directory` or `recursive` set to `true` ...

Should read,

> The `purge` parameter can only be used with `ensure` set to `directory` or `recurse` set to `true` ...

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

> The replace parameter should be used sparingly, but if set to `true`, allows for a file to have content enforced only if it does not exist. If the file exists, the state is met. This can be useful for applications that require an initial configuration file but then overwrite it.

Should read,

> The replace parameter should be used sparingly, but if set to `false`, allows for a file to have content enforced only if it does not exist ...

From the [Puppet 8 documentation](https://www.puppet.com/docs/puppet/8/types/file.html#file-attribute-replace):

> __replace__
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

Should read (correct 'in system terms' to 'in `systemd` terms'),

> Comparing this to `systemd`, the default provider for RHEL 8 and other Linux systems, we can see in the description under supported features that `systemctl` does not have delayed login or `manual` but does have `mask`, which, in `systemd` terms, means it disables the service so not even services that are dependent on it can activate it.

#### Page 49

The formatting for the legacy service example should be:

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

> The code can also be run in __noop mode__,

'mode' does not need to be in bold face.

The `grafana.ini` code example uses upper case key names; however, the [Grafana documentation](https://grafana.com/docs/grafana/latest/setup-grafana/configure-grafana/) use only lower case key names and should be formatted as:

```ini
[server]
protocol = HTTP
http_port = 8080
```

#### Page 52

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

:notebook: The statement,

> We can achieve this if the command itself is already idempotent, such as `apt-get update` ...

`apt-get update` is arguably _not_ idempotent as the command updates a catalog file after every run and may exit with a non-zero status.

In the paragraph,

> In the first case, if the command is idempotent, it will do no harm, but it will log in each Puppet run that it has run, and therefore using the other two methods is better to avoid the exec reporting runs.

It should reference "the other three methods ..." (`onlyif`, `unless`, and `creates`). If the language of the paragraph is referring to the use of `onlyif` then it should make it clear that "the first case" is `onlyif`.

In the `exec` code example for disabling public Chocolatey access, the hash rockets do not align. Indentation for both `exec` examples differ (pages 53 and 54). One use four spaces, the other uses three.

#### Page 54

There are too many spaces for the third `exec` code scenario. The example should be formatted as follows:

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

The parameterized `exec` code example has a typo for 'parameterized', has too many spaces and does not include a colon after the resource title.

The example should be formatted as follows:

```puppet
exec { 'parameterized command':
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

:notebook: The `notify` code example should have a space prior to the closing brace, as follows,

```puppet
notify { 'print a message to logs': }
```

#### Page 57

The `audit` code example has too many spaces and the resource title does not end with a colon. It should be formatted as follows:

```puppet
file { '/var/tmp/example':
  mode  => '0770',
  audit => [owner,group],
}
```

#### Page 58

The example code for `tag` has too many spaces before the hash rockets, the value for `ensure` need not be quoted. It should be formatted as follows:

```puppet
class example::access {
  group { 'ubuntu':
    ensure => present,
    gid    => 1000,
    tag    => ['pci','sox'],
  }
  user { 'ubuntu':
    ensure => present,
    tag    => 'pci',
  }
}
```

The `resources` metatype code example does not follow the [Puppet language style guide](https://www.puppet.com/docs/puppet/8/style_guide.html#style_guide_module_design-spacing) for spacing the resource title. It should be formatted as follows:

```puppet
resources { 'user':
  purge => true,
  noop  => true,
}
```

#### Page 59

Spacing in the array of titles code example is invalid and does not match the style guide. It should be formatted as follows:

```puppet
file { ['/opt/example1','/opt/example1/etc','/opt/example1/bin']:
  owner => 'user',
  group => 'user',
  mode  => '0750',
}
```

The overriding parameters code example has too many spaces before the hash rockets and no space between `File` and the overridden resource title. It should be formatted as follows:

```puppet
File ['/opt/example/bin/'] {
  group => 'other_group',
  audit => true,
}
```

#### Page 60

Indentation for the example `case` statement for the splat attribute is inconsistent; there are too many spaces before the hash rockets; the splat attribute references a brace-enclosed variable when it should not; and the quoted strings should use single quotes instead of double quotes. It should be formatted as follows:

```puppet
case $facts['os']['name'] {
  /^(Debian|Ubuntu)$/: {
    $package_options = {
      'name' => 'apache2'
    }
  }
  default: {
    $package_options = {
      'name' => 'httpd'
    }
  }
}
package { 'http':
  ensure => latest,
  *      => $package_options,
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

#### Page 61

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
  creates => '/tmp/badidea',
}
```

#### Page 62

:notebook: In the code example for the `default:` resource body, one array ends with a comma but the other does not.

The code example for the "Resource default syntax" uses a lower case 'f' for `file` instead of the upper case `File` as well as too many spaces before the hash rockets. The example should be formatted as follows:

```puppet
File {
  owner => 'exampleapp',
  group => 'exampleapp',
  mode  => '0660',
}
```

The `schedule` code examples also have too many spaces before or within the hash rockets and should be formatted as follows:

```puppet
schedule { 'Friday Night':
  day   => 'Friday',
  range => '18 - 9',
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

#### Page 63

:notebook: The statement,

> Exporting a resource just involves adding `@@` in front of a normal resource declaration.

Can be,

> Exporting a resource requires adding `@@` in front of a normal resource declaration.

The code example for exporting resources references a legacy fact and has too many spaces before the hash rockets. It should be formatted as follows:

```puppet
@@host { "Oracle database host entry ${trusted['hostname']}" :
  name => 'dbserver1',
  ip   => '192.168.0.6',
  tag  => 'oracle',
}
```

### Chapter 4

#### Page 69

In the Note at the beginning of the page, the statement,

> We are simplifying the process slightly here as there are now deferred functions that can run after complications.

Should read,

> We are simplifying the process slightly here as there are now deferred functions that can run after compilations.

Under the "Naming" heading, the sentence,

> The exception is regex capture variables, which are variables only named with numbers such as `$0`, `$1`, and so on.

Should read,

> The exception is regex capture variables, which are the only variables named with numbers such as `$0`, `$1`, and so on.

#### Page 70

:notebook: The `notify` code example under the "Interpolation" heading is missing spaces before and after the opening brace. It should be formatted as follows,

```puppet
notify { 'debug variable':
  message => "The database directory is ${database_directory}",
}
```

The code example under the "Data types" heading is missing the `$` variable prefix. It should be formatted as follows:

```puppet
class example (
  String $example_string = 'hello world',
  Integer $example_integer = 1,
) {
}
```

#### Page 71

The second sentence in the paragraph that begins with, "The next section will run ..." has an errant period between "types" and "so" that should be removed:

> Unfortunately, Puppet has no equivalent to the `puppet describe` command for data types .so all references ...

#### Page 72

:notebook: For the single quote example of the Windows path, it should be noted that the `file` resource documentation states,

> On Windows, the path should include the drive letter and should use `/` as the separator character (rather than `\`).

#### Page 73

The double-quoted string code example has the `file` resource opening brace _after_ the resource title. It should be formatted as follows:

```puppet
$make_file_content = "hello:\n\techo \"hello world\""

file { '/home/david/makefile':
  content => $make_file_content,
}
```

### Page 75

:notebook: All of the `notify` code examples on this page should have the the colon at the end of the resource title separated from the closing brace (`'title' :}` becomes `'title': }`).

The statement,

> For example, to extract the third character of a string variable, you would use an index of 3 (since indexing starts at 0).

Should be,

> For example, to extract the fourth character of a string variable, you would use an index of 3 (since indexing starts at 0).

Likewise, the sentence with,

> ... and you want to extract a substring that starts at the third character and includes the next five characters ...

Should be,

> ... and you want to extract a substring that starts at the fourth character and includes the next five characters ...

The paragraph,

> This would return the substring that starts at the fourth character from the end (which corresponds to the letter 't' in 'substring') and includes the next three characters, which in this case would be 'tri'.

Does not match the preceding code example,

```puppet
notify { "${example_string[-4,-1]}": }
```

It should be,

> This would return the substring that starts at the fourth character from the end (which corresponds to the letter 'r' in 'substring') and includes the next three characters, which in this case would be 'ing'.

### Page 76

The paragraph,

> This would return the substring that starts at the fourth character from the end (which corresponds to the letter 't' in 'substring') and includes the next four characters, which in this case would be 'ring'.

Which references the code example at the end of page 75:

```puppet
notify { "${example_string[-4,4]}": }
```

Should be,

> This would return the substring that starts at the fourth character from the end (which corresponds to the letter 'r' in 'substring') and includes the next three characters, which in this case would be 'ring'.

The code example for "... package names, application versions, or other consistent names ..." has an errant 'c' in the `$hostname` variable. It should be (comments added to show expected output),

```puppet
$hostname = flkoraprd00034
$location = $hostname[0,3] # flk
$role = $hostname[3,3] # ora
$env = $hostname[6,3] # prd
$id = $hostname[-5,5] # 00034
```

It should also be noted that the variable `$environment` is reserved and refers to the Puppet environment. I have taken the liberty of changing the variable in the example to `$env`.

:notebook: The formatting for the word 'string' at the end of the sentence,

> The default for the minimum is 0 and the maximum is infinity. To use the default implicitly, you can use the default unquoted string keyword.

Should be formatted with a monospace font and capitalized,

> The default for the minimum is 0 and the maximum is infinity. To use the default implicitly, you can use the default unquoted `String` keyword.

The code example for the 'database' class should not quote "database", is missing the `$` prefix for the variables, has an extra space after `'dbuser'`, and a colon after the closing brace that should not be there.

Puppet linters will also suggest that the `$description` variable precede the others.

It should be formatted:

```puppet
class database (
  String $description,
  String[4,4] $database_id,
  String[6,8] $username = 'dbuser',
) {
}
```

### Page 77

The `$scientific float = 3e5` example is missing an underscore and should be `$scientific_float = 3e5`.

The example `$hex = 0x` assigns an invalid number to the `$hex` variable. It should have some hexidecimal value after `0x`. For example, `$hex = 0x3a`.

### Page 78

:notebook: It should be noted that BODMAS is a region-specific (UK) acronym whereas other regions have different conventions: PEMDAS in the United States or BEDMAS in Canada, for example. What one region calls a bracket, another calls a parenthesis.

:notebook: I believe 'modulo' should be removed and substitute 'order of operation' for 'priority' in the sentence,

> Shifts are essentially treated as multiplication and modulo division in this priority.

:notebook: The subordinate clause seems to contradict the primary clause in this sentence,

> Any operations between an integer and a float will result in a float and an operation on an integer, which would result in a float being rounded down to an integer.

The use of 'which would' here should probably be changed to 'will':

... on an integer will result in ...

However, the sentence is unclear as to the outcome of integer and float operations. Will it be a float or a rounded down integer?

#### Page 79

:notebook: The code example at the top of the page may be easier to read with spaces surrounding the equal symbols. It could be formatted as,

```puppet
$string_integer = '1'
$string_float = '1.1'
$converted_integer = Integer($string_integer)
$converted_float = Float($string_float)
```

The code example for the `application::filesystem` class needs `$` prefixes for the variables and should be indented for readability.

It should be formatted:

```puppet
class application::filesystem (
  Float[0.1, 99.9] $percentage_application,
  Integer[100, 10000] $volume_group_size,
) {
}
```

#### Page 80

Indentation for the `notify` code example is further from the margin than other code examples in the book. In addition, the `$test1` variable should be enclosed in braces.

```puppet
notify { "Print ${test1}": }
```

:notebook: The sentence,

> The only value an `undef` data type has is the unquoted `undef` and it is not used for parameter data typing by itself. This is because enforcing the absence of a value would have no purpose.

Could be written,

> The value of an `undef` data type is the unquoted keyword `undef` and it is not used for parameter data typing by itself; enforcing the absence of a value has no purpose.

The code example for the boolean class `exampleapp` is missing the `$` variable prefix for `$manage_users`.

It should be formatted:

```puppet
class exampleapp (
  Boolean $manage_users = true,
) {
  $install_ssh = true
  $install_telnet = false
}
```

#### Page 82

Under the subsection, "Assigning arrays," the concluding sentence before the code example,

> For example, an array called `example_array` containing the `first`, `second`, and `third` strings, and would be declared as follows:

Should be,

> For example, an array called `$example_array` containing the strings `'first'`, `'second'`, and `'third'` is declared as follows:

:notebook: The mixed array code example has an errant space and should be formatted as,

```puppet
$example_boolean = false
$mixed_example_array = [ 1, $example_boolean, 'example' ]
```

In the "Accessing an array index" code example, there is a space between the variable `$second_index` and the index `[1]`. It should be formatted as:

```puppet
$example_array = [ 'first','second','third' ]
$second_index = $example_arrary[1]
```

In the `notify` example, 'first' should instead be 'third'; it also has mis-matched spacing and should be formatted as:

```puppet
notify { "The third element is ${example_array[-1]}": }
```

The sentence at the end of the page is incomplete. It may be sufficient to simply state that a space between the variable and the opening bracket will result in a syntax error.

> You mustn’t put any spacing between the square bracket and the variable name; otherwise, it will be interpreted as a variable and the square brackets will be separate.

Could be written as,

> Any whitespace between the variable name and the opening square bracket will result in a syntax error.

#### Page 83

The `$sub_array` code example has one too many spaces following the `=` symbol and the reference to `$example_array` is missing the `$` variable prefix. It should be formatted as:

```puppet
$sub_array = $example_array[1,1]
```

All of the negative length code examples are missing the `$` variable prefix for the `$example_array`. It should be formatted as:

```puppet
$negative_sub_array = $example_array[0, -1]
$empty_sub_array = $example_array[1, -3]
$second_element_array = $example_array[1, -2]
```

In the nested array code example, if the line for `$nest_second` is to return the string 'nest_second' it should be formatted as:

```puppet
$nest_second = $nested_array[1][1]
```

The sentence,

> For example, the following `notify` resource will print the first element of `nested_array`:

With the code example,

```puppet
notify {"Print ${nested_array[1][0]}":}
```

Should either be written to refer to the _second_ element,

> For example, the following `notify` resource will print the second element of `$nested_array`:

Or the code example changed thus to refer to the first element:

```puppet
notify { "Print ${nested_array[0][0]}": }
```

If the intent was to demonstrate that the `notify` resource will print the first element of the _nested_ array, it should be written as,

> For example, the following `notify` resource will print the first element of the nested array:

With the corrected code referring to index `[1][0]`.

#### Page 84

In the paragraph under the _Append_ heading, the number '3' should be the string `'three'`,

> To demonstrate this, let’s look at an example of an array with integers 1 and 2 as elements that appends ~~3~~ `'three'` into a new array.

:notebook: The code example,

```puppet
$example_array=[1,2]
$new_array=$example_array << 'three'
$append_nest=$example_array << [3,4]
```

Should have spaces before and after the equal symbol:

```puppet
$example_array = [1,2]
$new_array = $example_array << 'three'
$append_nest = $example_array << [3,4]
```

#### Page 85

The second line of the hash concatenation code example,

```puppet
$nested_hash =$example_array + [{test => 'value'}]
```

Should have a space after the equal symbol,

```puppet
$nested_hash = $example_array + [{test => 'value'}]
```

#### Page 86

The `database` class code example should not quote the class name, there should be no following colon, `default` should be `Default`, `string` should be `String`, the variables need the `$` prefix, and the entire variable block should be enclosed by parentheses.

It should be formatted as:

```puppet
class database (
  Array[Default,1,6] $db_uids,
  Array[String,0,5] $user_names,
  Array $extra_flags,
) {
}
```

The paragraph under the "Assigning hashes" heading has several typos.

> Hashes are written as comma-spaced key-value pairs separated by `=>` and the list is surrounded by curl braces, `{ }`. A trailing comma can be added after the last pair, but this is not a recommended style by this book. For example, the following hash pairs could be declined to assign the `make` key with the `skoda` string, the `model` key with the `rapid` string, and the `year` key with the `2014` integer:

Should be,

> Hashes are written as comma separated key-value pairs where values are assigned to keys with `=>` and the list is surrounded by curly braces, `{ }`. A trailing comma should be added after the last pair, but this is not a style recommended by this book.
>
> For example, the following hash can be declared to assign the `make` key with the `'skoda'` string, the `model` key with the `'rapid'` string, and the `year` key with the `2014` integer:

#### Page 87

The sentence in the opening paragraph uses 'arrays' instead of 'hashes'.

> Taking a final new line for the closing curly brace and lining it up with the opening curly brace is what this book recommends when writing arrays:

Should be,

> Taking a final new line for the closing curly brace and lining it up with the opening curly brace is what this book recommends when writing hashes:

:notebook: The [Puppet language style guide's](https://www.puppet.com/docs/puppet/8/style_guide.html#arrays-hashes) recommendation for arrays and hashes is easier to read than the style recommended by this book. It also reduces the size on disk of Puppet files.

```puppet
$my_car = { make  => 'skoda',
            model => 'rapid',
            year  => 2014
          }
```

Should be formatted as:

```puppet
$my_car = {
  make  => 'skoda',
  model => 'rapid',
  year  => 2014,
}
```

The `$package_list` hash example under the "Nested hashes" heading is missing a comma separating the `packages` and `services` hashes and has misaligned hash rockets.

It should be formatted as:

```puppet
$package_list = {
  packages => {
    httpd  => 'latest',
    cowsay => 4.0,
  },
  services => {
    httpd => 'running',
    nginx => 'stopped',
  }
}
```

#### Page 88

:notebook: There are too many spaces in the "_Merging_" and "_Removal_" code examples.

#### Page 89

The `$tunables` variable in the `kernel_overrides` class example is missing the `$` variable prefix, the `integer` entry should be `Integer`, and the required curly braces `{ }`.

It should be formatted as:

```puppet
class kernel_overrides (
  Hash[String,Integer,1,10] $tunables,
) {
}
```

The first sentence under the heading "Mixing hashes and arrays" should drop the second use of the word 'value'; for 'array value' can be 'array element' instead.

> Since the value of a hash key value or an array value can be any data type, nesting can be performed.

Should be:

> Since the value of a hash key or an array element can be any data type, nesting can be performed.

#### Page 90

:notebook: The hash rockets in the `user` resource code example do not align.

:notebook: I am uncertain what meaning this sentence is supposed to convey.

> If only the unwrap is performed when running Puppet with debug, the command and password would be fully visible.

#### Page 91

The opening phrase to the following paragraph seems to use the word 'pattern' one too many times. At the end of the paragraph, `string` should be `String`.

> `Enum` and more advanced pattern data type patterns, which will be covered in the next section, will not work with `Sensitive` and should be avoided. Here, you should only use basic types such as `string`.

Suggested,

> The next section covers more advanced data types that do not work with `Sensitive` and should be avoided. Use only basic data types such as `String`.

Alternatively, remove the paragraph entirely and note the warning in the relevant section.

#### Page 92

The sentence under the "Arrays and hashes" heading,

> In this section, we will cover the various arrays and hashes types.

Should be,

> In this section, we will cover the various array and hash types.

#### Page 93

The sentence,

> The `user_declaration` variable requires a string for the username, an integer for the UID, and at least one string up to eight characters in length, which represents the groups that a user can be assigned to.

Does not agree with the code example. It claims "one string up to eight characters" but the code example has no reference to eight. The way the example is written, it defines the `$user_declaration` variable as an array comprising a `String`, an `Integer`, and another `String` with a minimum of those three elements and a maximum of ten `String` type elements (the last defined type).

The `Tuple` code example class does not use upper case type definitions, lacks the `$` variable prefix, has spaces between `Tuple` and the opening square bracket, has several errant spaces, and is missing the 'n' in `$file_download`.

It should be formatted as:

```puppet
class exampleapp (
  Tuple[ String, Integer, String, 3, 10 ] $user_declaration,
  Tuple[ Integer, Float, Integer ] $calculation,
  Tuple[ Uri, String, Integer, 2 ] $file_download,
) {
}
```

The `skeleton` class example for the `Struct` data type is missing the `$` variable prefix, has extra spaces between hash rockets, and is missing commas after each `Struct` definition.

It should be formatted as:

```puppet
class skeleton (
  Struct[
    {
      mode => Enum[file, link],
      path => String,
    }
  ] $config_file,
  Struct[
    {
      mode            => Enum[file, link],
      path            => String,
      Optional[owner] => String,
    }
  ] $application_binary,
  Struct[
    {
      mode  => Enum[file, link],
      path  => String,
      owner => Optional[String]
    }
  ] $application_startup,
) {
}
```

### Chapter 5

### Chapter 6

### Chapter 7

### Chapter 8

### Chapter 9

### Chapter 10

### Chapter 11

### Chapter 12

### Chapter 13

### Chapter 14

### Chapter 15
