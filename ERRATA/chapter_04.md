# Chapter 4

## Page 69

In the Note at the beginning of the page, the statement,

> We are simplifying the process slightly here as there are now deferred functions that can run after complications.

Should read,

> We are simplifying the process slightly here as there are now deferred functions that can run after compilations.

---

Under the "Naming" heading, the sentence,

> The exception is regex capture variables, which are variables only named with numbers such as `$0`, `$1`, and so on.

Should read,

> The exception is regex capture variables, which are the only variables named with numbers such as `$0`, `$1`, and so on.

---

## Page 70

:notebook: The `notify` code example under the "Interpolation" heading is missing spaces before and after the opening brace. It should be formatted as follows,

```puppet
notify { 'debug variable':
  message => "The database directory is ${database_directory}",
}
```

---

The code example under the "Data types" heading is missing the `$` variable prefix. It should be formatted as follows:

```puppet
class example (
  String $example_string = 'hello world',
  Integer $example_integer = 1,
) {
}
```

---

## Page 71

The second sentence in the paragraph that begins with, "The next section will run ..." has an errant period between "types" and "so" that should be removed:

> Unfortunately, Puppet has no equivalent to the `puppet describe` command for data types .so all references ...

---

## Page 72

:notebook: For the single quote example of the Windows path, it should be noted that the `file` resource documentation states,

> On Windows, the path should include the drive letter and should use `/` as the separator character (rather than `\`).

---

## Page 73

The double-quoted string code example has the `file` resource opening brace *after* the resource title. It should be formatted as follows:

```puppet
$make_file_content = "hello:\n\techo \"hello world\""

file { '/home/david/makefile':
  content => $make_file_content,
}
```

---

## Page 75

:notebook: All of the `notify` code examples on this page should have the the colon at the end of the resource title separated from the closing brace (`'title' :}` becomes `'title': }`).

---

The statement,

> For example, to extract the third character of a string variable, you would use an index of 3 (since indexing starts at 0).

Should be,

> For example, to extract the fourth character of a string variable, you would use an index of 3 (since indexing starts at 0).

Likewise, the sentence with,

> ... and you want to extract a substring that starts at the third character and includes the next five characters ...

Should be,

> ... and you want to extract a substring that starts at the fourth character and includes the next five characters ...

---

The paragraph,

> This would return the substring that starts at the fourth character from the end (which corresponds to the letter 't' in 'substring') and includes the next three characters, which in this case would be 'tri'.

Does not match the preceding code example,

```puppet
notify { "${example_string[-4,-1]}": }
```

It should be,

> This would return the substring that starts at the fourth character from the end (which corresponds to the letter 'r' in 'substring') and includes the next three characters, which in this case would be 'ing'.

---

## Page 76

The paragraph,

> This would return the substring that starts at the fourth character from the end (which corresponds to the letter 't' in 'substring') and includes the next four characters, which in this case would be 'ring'.

Which references the code example at the end of page 75:

```puppet
notify { "${example_string[-4,4]}": }
```

Should be,

> This would return the substring that starts at the fourth character from the end (which corresponds to the letter 'r' in 'substring') and includes the next three characters, which in this case would be 'ring'.

---

The code example for "... package names, application versions, or other consistent names ..." has an errant 'c' in the `$hostname` variable. It should be (comments added to show expected output),

```puppet
$hostname = flkoraprd00034
$location = $hostname[0,3] # flk
$role = $hostname[3,3] # ora
$env = $hostname[6,3] # prd
$id = $hostname[-5,5] # 00034
```

It should also be noted that the variable `$environment` is reserved and refers to the Puppet environment. I have taken the liberty of changing the variable in the example to `$env`.

---

:notebook: The formatting for the word 'string' at the end of the sentence,

> The default for the minimum is 0 and the maximum is infinity. To use the default implicitly, you can use the default unquoted string keyword.

Should be formatted with a monospace font and capitalized,

> The default for the minimum is 0 and the maximum is infinity. To use the default implicitly, you can use the default unquoted `String` keyword.

---

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

---

## Page 77

The `$scientific float = 3e5` example is missing an underscore and should be `$scientific_float = 3e5`.

The example `$hex = 0x` assigns an invalid number to the `$hex` variable. It should have some hexidecimal value after `0x`. For example, `$hex = 0x3a`.

---

## Page 78

:notebook: It should be noted that BODMAS is a region-specific (UK) acronym whereas other regions have different conventions: PEMDAS in the United States or BEDMAS in Canada, for example. What one region calls a bracket, another calls a parenthesis.

---

:notebook: I believe 'modulo' should be removed and substitute 'order of operation' for 'priority' in the sentence,

> Shifts are essentially treated as multiplication and modulo division in this priority.

---

:notebook: The subordinate clause seems to contradict the primary clause in this sentence,

> Any operations between an integer and a float will result in a float and an operation on an integer, which would result in a float being rounded down to an integer.

The use of 'which would' here should probably be changed to 'will':

... on an integer will result in ...

However, the sentence is unclear as to the outcome of integer and float operations. Will it be a float or a rounded down integer?

---

## Page 79

:notebook: The code example at the top of the page may be easier to read with spaces surrounding the equal symbols. It could be formatted as,

```puppet
$string_integer = '1'
$string_float = '1.1'
$converted_integer = Integer($string_integer)
$converted_float = Float($string_float)
```

---

The code example for the `application::filesystem` class needs `$` prefixes for the variables and should be indented for readability.

It should be formatted:

```puppet
class application::filesystem (
  Float[0.1, 99.9] $percentage_application,
  Integer[100, 10000] $volume_group_size,
) {
}
```

---

## Page 80

Indentation for the `notify` code example is further from the margin than other code examples in the book. In addition, the `$test1` variable should be enclosed in braces.

```puppet
notify { "Print ${test1}": }
```

---

:notebook: The sentence,

> The only value an `undef` data type has is the unquoted `undef` and it is not used for parameter data typing by itself. This is because enforcing the absence of a value would have no purpose.

Could be written,

> The value of an `undef` data type is the unquoted keyword `undef` and it is not used for parameter data typing by itself; enforcing the absence of a value has no purpose.

---

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

---

## Page 82

Under the subsection, "Assigning arrays," the concluding sentence before the code example,

> For example, an array called `example_array` containing the `first`, `second`, and `third` strings, and would be declared as follows:

Should be,

> For example, an array called `$example_array` containing the strings `'first'`, `'second'`, and `'third'` is declared as follows:

---

:notebook: The mixed array code example has an errant space and should be formatted as,

```puppet
$example_boolean = false
$mixed_example_array = [ 1, $example_boolean, 'example' ]
```

---

In the "Accessing an array index" code example, there is a space between the variable `$second_index` and the index `[1]`. It should be formatted as:

```puppet
$example_array = [ 'first','second','third' ]
$second_index = $example_arrary[1]
```

---

In the `notify` example, 'first' should instead be 'third'; it also has mis-matched spacing and should be formatted as:

```puppet
notify { "The third element is ${example_array[-1]}": }
```

---

The sentence at the end of the page is incomplete. It may be sufficient to simply state that a space between the variable and the opening bracket will result in a syntax error.

> You mustn’t put any spacing between the square bracket and the variable name; otherwise, it will be interpreted as a variable and the square brackets will be separate.

Could be written as,

> Any whitespace between the variable name and the opening square bracket will result in a syntax error.

---

## Page 83

The `$sub_array` code example has one too many spaces following the `=` symbol and the reference to `$example_array` is missing the `$` variable prefix. It should be formatted as:

```puppet
$sub_array = $example_array[1, 1]
```

---

All of the negative length code examples are missing the `$` variable prefix for the `$example_array`. It should be formatted as:

```puppet
$negative_sub_array = $example_array[0, -1]
$empty_sub_array = $example_array[1, -3]
$second_element_array = $example_array[1, -2]
```

---

In the nested array code example, if the line for `$nest_second` is to return the string 'nest_second' it should be formatted as:

```puppet
$nest_second = $nested_array[1][1]
```

---

The sentence,

> For example, the following `notify` resource will print the first element of `nested_array`:

With the code example,

```puppet
notify {"Print ${nested_array[1][0]}":}
```

Should either be written to refer to the *second* element,

> For example, the following `notify` resource will print the second element of `$nested_array`:

Or the code example changed thus to refer to the first element:

```puppet
notify { "Print ${nested_array[0][0]}": }
```

If the intent was to demonstrate that the `notify` resource will print the first element of the *nested* array, it should be written as,

> For example, the following `notify` resource will print the first element of the nested array:

With the corrected code referring to index `[1][0]`.

---

## Page 84

In the paragraph under the *Append* heading, the number '3' should be the string `'three'`,

> To demonstrate this, let’s look at an example of an array with integers 1 and 2 as elements that appends ~~3~~ `'three'` into a new array.

---

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

---

## Page 85

The second line of the hash concatenation code example,

```puppet
$nested_hash =$example_array + [{test => 'value'}]
```

Should have a space after the equal symbol,

```puppet
$nested_hash = $example_array + [{test => 'value'}]
```

---

## Page 86

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

---

The paragraph under the "Assigning hashes" heading has several typos.

> Hashes are written as comma-spaced key-value pairs separated by `=>` and the list is surrounded by curl braces, `{ }`. A trailing comma can be added after the last pair, but this is not a recommended style by this book. For example, the following hash pairs could be declined to assign the `make` key with the `skoda` string, the `model` key with the `rapid` string, and the `year` key with the `2014` integer:

Should be,

> Hashes are written as comma separated key-value pairs where values are assigned to keys with `=>` and the list is surrounded by curly braces, `{ }`. A trailing comma should be added after the last pair, but this is not a style recommended by this book.
>
> For example, the following hash can be declared to assign the `make` key with the `'skoda'` string, the `model` key with the `'rapid'` string, and the `year` key with the `2014` integer:

---

## Page 87

The sentence in the opening paragraph uses 'arrays' instead of 'hashes'.

> Taking a final new line for the closing curly brace and lining it up with the opening curly brace is what this book recommends when writing arrays:

Should be,

> Taking a final new line for the closing curly brace and lining it up with the opening curly brace is what this book recommends when writing hashes:

---

:notebook: The [Puppet language style guide's](https://www.puppet.com/docs/puppet/8/style_guide.html#arrays-hashes) recommendation for arrays and hashes is easier to read than the style recommended by this book. It also reduces the size on disk of Puppet files.

```puppet
$my_car = { make  => 'skoda',
            model => 'rapid',
            year  => 2014
          }
```

Should be formatted as:

```puppet
$my_car = {
  make  => 'skoda',
  model => 'rapid',
  year  => 2014,
}
```

---

The `$package_list` hash example under the "Nested hashes" heading is missing a comma separating the `packages` and `services` hashes and has misaligned hash rockets.

It should be formatted as:

```puppet
$package_list = {
  packages => {
    httpd  => 'latest',
    cowsay => 4.0,
  },
  services => {
    httpd => 'running',
    nginx => 'stopped',
  }
}
```

---

## Page 88

:notebook: There are too many spaces in the "*Merging*" and "*Removal*" code examples.

---

## Page 89

The `$tunables` variable in the `kernel_overrides` class example is missing the `$` variable prefix, the `integer` entry should be `Integer`, and the required curly braces `{ }`.

It should be formatted as:

```puppet
class kernel_overrides (
  Hash[String,Integer,1,10] $tunables,
) {
}
```

---

The first sentence under the heading "Mixing hashes and arrays" should drop the second use of the word 'value'; for 'array value' can be 'array element' instead.

> Since the value of a hash key value or an array value can be any data type, nesting can be performed.

Should be:

> Since the value of a hash key or an array element can be any data type, nesting can be performed.

---

## Page 90

:notebook: The hash rockets in the `user` resource code example do not align.

---

:notebook: I am uncertain what meaning this sentence is supposed to convey.

> If only the unwrap is performed when running Puppet with debug, the command and password would be fully visible.

---

## Page 91

The opening phrase to the following paragraph seems to use the word 'pattern' one too many times. At the end of the paragraph, `string` should be `String`.

> `Enum` and more advanced pattern data type patterns, which will be covered in the next section, will not work with `Sensitive` and should be avoided. Here, you should only use basic types such as `string`.

Suggested,

> The next section covers more advanced data types that do not work with `Sensitive` and should be avoided. Use only basic data types such as `String`.

Alternatively, remove the paragraph entirely and note the warning in the relevant section.

---

## Page 92

The sentence under the "Arrays and hashes" heading,

> In this section, we will cover the various arrays and hashes types.

Should be,

> In this section, we will cover the various array and hash types.

---

## Page 93

The sentence,

> The `user_declaration` variable requires a string for the username, an integer for the UID, and at least one string up to eight characters in length, which represents the groups that a user can be assigned to.

Does not agree with the code example. It claims "one string up to eight characters" but the code example has no reference to eight. The way the example is written, it defines the `$user_declaration` variable as an array comprising a `String`, an `Integer`, and another `String` with a minimum of those three elements and a maximum of ten `String` type elements (the last defined type).

---

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

---

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
      mode            => Enum[file, link],
      path            => String,
      Optional[owner] => String,
    }
  ] $application_binary,
  Struct[
    {
      mode  => Enum[file, link],
      path  => String,
      owner => Optional[String]
    }
  ] $application_startup,
) {
}
```

---

## Page 94

The sentences in the paragraph under the Scope heading,

> ... For example, variables can be declared in the site.pp manifest file within a Puppet environment to make them globally available to all nodes. Alternatively, variables can be declared in a node definition in site.pp or the ENC to be made available at the node level for a particular server or group of servers. ...

Are redundant restatements of the sentences preceding them.

---

## Page 95

:notebook: In the sentence,

> ... We will use two notify resources to demonstrate how variable scope works.

'variable scope' could mean variations with scope. A more concise phrase is "how scope works with Puppet variables."

---

:notebook: The following sentence,

> The first notify resource prints '`Print override`', showing that the '`global`' local variable has overridden the global value.

Should be written,

> The first notify resource prints '`Print override`', showing that the local variable '`global`' has overridden the global value.

Thus making the scope of the `global` variable more clear.

---

> The third notify resource prints '`Print node`' ...

Should be,

> The third notify resource prints '`Print mynode`' ...

---

In the sentence,

> In the '`also_local`' class, we define a new variable called '`another_global`' with a string value of '`another world`'.

Neither the variable `$another_global` nor the value `another world` are used.

---

:notebook: The example code uses the variable `$node`, which is a reserved word. While it is allowed, it should be avoided.

The example code for the `local` class:

```puppet
class local
{
$global = 'override'
  notify {"Print ${global}":}
  notify {"Print ${::global}":}
  notify {"Print ${node}":}
}
```

Should be formatted,

```puppet
class local {
  $global = 'override'
  notify { "Print ${global}": }
  notify { "Print ${::global}": }
  notify { "Print ${node}": }
}
```

---

## Page 96

The use of "After" to begin the sentence,

> After, we reviewed how Puppet variables can be declared at different scopes and how variables can be shared/seen in different scopes.

Should instead be "Finally" as it is the final summary element.

---

In the sentence in the final paragraph that begins,

> We will cover built-in functions and functions from the standard `lib` module, from Puppet Forge ...

The reference to "standard `lib`" should be "`stdlib`".
