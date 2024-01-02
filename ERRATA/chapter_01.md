# Chapter 1

## Page 6

The code example has two typos:

* Line 1: `user { 'david'` should instead be `user { 'david':`
* Line 2: `uid => '123'` should instead be `uid => '123',`

---

## Pages 7-8

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

---

## Page 10

The sentence ending,

> ... modules provide sharable and reusable single-use technical installations.

should read,

> ... modules provide sharable and reusable single-use technical implementations.

---

## Page 11

The code examples have one typo each:

`profile::os_security:email_enabled: true` should instead be: `profile::os_security::email_enabled: true`

`profile::exampleapp:uid: '1235'` should instead be: `profile::exampleapp::uid: '1235'`

---

:notebook: The sentence,

> One of the most important points of creating these patterns is to avoid hardcoded values in your modules.

conflicts somewhat with the sentence from chapter 9,

> The first key thing is if the data doesn't vary over nodes and it's only used once, the simplest thing is to hardcode the data in Puppet code ...

---

## Page 15

The code example has two typos:

* Line 2 `:git => 'https://github.com/exampleorg/exampleapp'` should instead be `:git => 'https://github.com/exampleorg/exampleapp.git',`

---

:notebook: The sentence,

> Normally, this means a minimum of a development environment and a production environment. So, changes can be tested against servers in development, and then successfully tested ones can be deployed to production.

should instead be,

> Normally, this means a minimum of a development environment and a production environment to test changes against servers in development, with successfully tested ones subsequently deployed to production.

---

:notebook: The reference to the latest version of Puppet should be changed from 7 to 8. All installation URIs appear to use Puppet 8 even though the Azure lab installs Puppet 7.
