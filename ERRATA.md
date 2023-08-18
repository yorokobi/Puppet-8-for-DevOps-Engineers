## Errata

Entries with :notebook: are my opinion.

#### Page 39:

The code example has two typos:

* Line 1: `user { 'david'` should instead be `user { 'david':`
* Line 2: `uid => '123'` should instead be `uid => '123',`

#### Page 41:

The code example should be as follows:

```
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

#### Page 44:

The sentence ending "modules provide sharable and reusable single-use technical installations." should probably read "modules provide sharable and reusable single-use technical implementations."

#### Page 45:

The code examples have one typo each:

`profile::os_security:email_enabled: true` should instead be:
`profile::os_security::email_enabled: true`

`profile::exampleapp:uid: '1235'` should instead be:
`profile::exampleapp::uid: '1235'`

:notebook: Reader's comment for page 45:

The sentence, "One of the most important points of creating these patterns is to avoid hardcoded values in your modules." conflicts somewhat with the sentence from chapter 9, "The first key thing is if the data doesn't vary over nodes and it's only used once, the simplest thing is to hardcode the data in Puppet code ..."

#### Page 50:

The code example has two typos:

* Line 2 `:git => 'https://github.com/exampleorg/exampleapp'` should instead be `:git => 'https://github.com/exampleorg/exampleapp.git',`

:notebook: Reader's comment for page 50:

The sentence, "Normally, this means a minimum of a development environment and a production environment. So, changes can be tested against servers in development, and then successfully tested ones can be deployed to production." should instead be, "Normally, this means a minimum of a development environment and a production environment so changes can be tested against servers in development and then successfully tested ones can be deployed to production."

:notebook: Reader's comment for page 53:

The reference to the latest version of Puppet should be changed from 7 to 8. All installation URIs appear to use Puppet 8 even though the Azure lab installs Puppet 7.

#### Page 56:

The bullet point:

* A Linux environment using package managers such as apt for Ubuntu or RHEL-based using Yum. 

Should instead be:

* A Linux environment using package managers such as apt/apt-get for Debian based distributions or yum/dnf for Red Hat based distributions.

The final bullet point for Visual Studio Code extensions references an application unrelated to VSCode: `pecdm`. The bullet point should be shifted left to align with "The GitHub CLI" etc.

#### Page 61:

"Augeas" is misspelled in the sentence:

> "Augeuas is very advanced but often over-complicated ..."

:notebook: Reader's comment for pages 62-63:

The ending of the following sentence lacks a proper subject for what to develop and what to integrate with: 

> One of the greatest issues with early Puppet development was the lack of a consensus around how to develop and a lack of integration.

The sentence,

> This is certainly not the only way to develop Puppet code, and your organization might require the usage of different tools deponding on the environment.

Can be written,

> This is certainly not the only way to develop Puppet code and your organization might require using different tools, depending on the environment.

The claim that PDK will be covered "in full" in chapter 8 is misleading as PDK is not covered "in full" in that chapter.

Vim is referenced twice, once as 'Vim' and, in the same sentence, as 'VIM.' 'Vim' is correct as it is not an acronym.

The sentence ending,

> ... to avoid paying for unecessary virtual machine running time costs on Azure.

can be simplified (and the typo "unecessary" corrected) to,

> ... to avoid paying for unnecessary virtual machine time on Azure.

#### Page 63:

The URL for `https://validate.puppet.com/` is not valid. No such website exists. This is referenced on pages 63, 86, 207, and 224.

:notebook: Reader's comment for page 66:

References to 'Yum' or 'yum' should be replaced with 'dnf' as Red Hat Enterprise Linux 8+ (and related distributions) use 'dnf' by default. This is also true of the package provider for these distributions.

#### Page 69:

The code example has one typo:

* Line 1: `mkdir ~workspace/pecdm` should instead be `mkdir -p ~workspace/pecdm`

:notebook: Reader's comment for page 69:

`~workspace` should be `~/workspace`. Example: `mkdir -p ~/workspace/pecdm`

#### Page 73:

This sentence needs a space after the first comma:

> Puppet has its own learning site (https://training.puppet.com/learn),this ...

It should be:

> Puppet has its own learning site (https://training.puppet.com/learn), this ...

The sentence,

> Puppet's support knowledge base was made public in April 2022, ...

should be a new paragraph.

The sentence,

> Puppet previously run two, ... which had to be paid for and lasted 3 ...

Should instead be,

> Puppet previously ran two, ... which had to be paid for and lasted three ...

In the paragraph that begins, "The key difference is that" the two words "self paced" should be hyphenated as "self-paced"

:notebook: Reader's comment for page 74:

The paragraph beginning,

> This section is not supposed to be an exhaustive ...

Can be simplified to,

> This section is not an exhaustive ...
