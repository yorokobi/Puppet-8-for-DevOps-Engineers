# Chapter 7

## Page 147

In Table 7.1, the ending tag with trimming for non-printing expressions should be `-%>`, not `<%-`.

---

The paragraph,

> For example, to have an options parameter containing a string set to an empty string by default, an `application_mode` parameter, which can contain full, partial, or none strings and defaults to `node`, and a `cluster_enabled` parameter, which is a Boolean, the following code would start our template:

Should read,

> For example, the `$options` parameter contains an empty string by default. The `$application_mode` parameter, which contains one of the enumerated strings 'full', 'partial', or 'none', defaults to 'none'. Finally, the Boolean `$cluster_enabled` parameter has no default. The following code starts our template:

---

## Page 148

There is no function `epp_template()` as mentioned in the sentence,

> Later in this section, it will be seen how to pass a hash to the `epp_template` function when referencing it.

The EPP template functions are `epp()` and `inline_epp()`.

---

:notebook: In the code examples on pages 148 and 149, I would replace `-%>` with `%>` to preserve the line ending.

```puppet
application = <%= $facts[application_name] -%>
```

Should be,

```puppet
application = <%= $facts[application_name] %>
```

---

## Page 149

The sentence,

> For instance, to output `<% Puppet expression example %>` as text, you would write `<%% Puppet expression example %%%>`.

Should be,

> For instance, to output `<% Puppet expression example %>` as text, you would write `<%% Puppet expression example %>`.

The closing template tag requires one `%` since the opening `<%%` indicates the remainder of the line is literal. See <https://www.puppet.com/docs/puppet/8/lang_template_epp.html#epp_tags-epp-literal-tag-delimiters>.

---

## Page 150

The `epp()` code example has misaligned hash rockets and the `content` parameter values should span multiple lines for readability.

It should be formatted,

```puppet
file { '/etc/exampleapp.conf':
  ensure  => file,
  content => epp('exampleapp/exampleapp.conf.epp',
    {
      'version'   => '1',
      'clustered' => false,
    }
  ),
}
```

---

The Hashicorp Vault code example also has misaligned hash rockets, uses double quotes for `'secret/exampleapp'` (which is also mispelled), and should employ multiple lines for the `epp()` parameters as well as for the `$vault_keypair` hash.

It should be formatted,

```puppet
$vault_keypair = {
  'password' => Deferred('vault_lookup::lookup',
    [
      'secret/exampleapp',
      'https://vault:8200',
    ]
  ),
}
file { '/etc/exampleapp_secret.conf':
  ensure  => file,
  content => Deferred('inline_epp',
    [
      'PASSWORD=<%= $password.unwrap %>',
      $vault_keypair,
    ]
  ),
}
```

---

:notebook: Shouldn't the sentence,

> Having covered EPP templates for the management of heritage code, we will now review how ERB is different.

instead read,

> Having covered ERB templates for the management of heritage code, we will now review how EPP is different.

as ERB is "heritage code," not EPP?

---

## Page 152

The hash rockets in the first code example for the `template()` function do not align.

---

## Page 155

The sentence,

> This would result in the notice function printing for each string in the array, similar to a for loop with a print/echo command in most languages.

Should read,

> This results in the `notice()` function printing each string in the array, similar to a `for` loop with a `print()` function or `echo` command in most languages.

---

The example code for the `each()` function receiving two parameters requires a comma between the two parameters.

It should be formatted,

```ruby
['first', 'second', 'third'].each | $index, $value | {
  notice "index $index contains $value"
}
```

---

There is a period missing at the end of the sentence,

> ... will output two strings, one for each key-value pair: `key1 contains val1` and `key2 contains val2`

---

## Page 156

In the second `slice()` example lambda, three parameters are used but the `notice()` function is passed `$numbers`, which is not part of the lambda definition.

```ruby
Integer[100, 151].slice(3) | Integer $first, Integer $second, Integer $third | { notice $numbers }
```

---

## Page 158

The example for the `then()` function uses an incorrect array index for the change to the 'd' element.

The relevant dialog should be formatted,

> ... The following example uses the `dig()` function to attempt to access a 'c' element that does not exist in the second hash in the array. It will receive `undef` and, therefore, return `undef`:

```ruby
$example = { first => { second => [ { a => 10, b => 20, }, { d => 30, e => 40, } ] } }
$example.dig(first, second, 1, c).then |$x| { $x / 10 }.notice()
```

> To clarify the previous statement, changing `dig(first, second, 1, c)` to `dig(first, second, 1, d)`, will pass `30` to the lambda, divide it by `10`, and print `3`.

---

:notebook: This sentence needs clarification or removal.

> The `with` function is somewhat of a specialist edge, as it is used to pass values through if our lambda is able to handle `undef` or defined values.

---

## Page 159

The opening sentence under the "Conditional statements" heading,

> Puppet has the conditional statements you would expect of any language ...

Should read,

> Puppet has several of the conditional statements you would expect of any language ...

---

None of the `if`, `else`, `elsif`, and `unless` examples on pages 159 and 160 meet the Puppet language style guide for [conditional statement alignment](https://www.puppet.com/docs/puppet/8/style_guide.html#conditional-statement-alignment).

For example,

```puppet
if $example_bool {
notice 'It was true'
}else{
  notice 'It was false'
}
```

Should be formatted,

```puppet
if $example_bool {
  notice 'It was true'
} else {
  notice 'It was false'
}
```

---

## Page 161

The `case` example references the deprecated fact `$facts['hardwareisa']`. It should use `$facts['os']['hardware']` or `$facts['os']['architecture']` instead.

---

The hash rockets in the code example for `$apache_package_name` do not align, there are errant spaces for the `/(Debian|Ubuntu)/` entry, and the colon demarking the `package` resource title is missing.

It should be formatted,

```puppet
$apache_package_name = $facts['os']['family'] ? {
  'RedHat'          => 'httpd',
  /(Debian|Ubuntu)/ => 'apache2',
  'Windows'         => 'apache-httpd',
  default           => 'httpd',
}
package { $apache_package_name: }
```

---

## Page 162

:notebook: The sentence,

> Having reviewed all aspects of templates, conditionals, iterations, and loops, we will now use a lab to recap and bring these concepts together.

Is ... ambitious. *Many* of the aspects of templates, conditionals, etc. were reviewed. Certainly not *all*.

---

:notebook: The sentence,

> In this lab, we will bring together everything you have seen in this chapter so far ...

So far? This is the beginning of the lab before the chapter summary. There is no more of the chapter to "bring together."

---

For Lab 2, the following should be bullet points and use fewer quotes.

:notebook: Replace all so-called "smart" quotes with plain quotes.

> “This is a < os family > machine running version < os release full > ““The following directories are in the path < list each path >”

Should be,

> - "This is a < os.family > machine running version < os.release.full >"
> - "The following directories are in the path: < list each path >"
