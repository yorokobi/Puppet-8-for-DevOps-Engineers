# Chapter 5

## Page 99

:notebook: In the sentence,

> When Puppet is run, either via the agent or by running `puppet apply` on the command line, Facter will run, with legacy facts, disabled in Puppet 8 or enabled in Puppet 7 and below and the output will be assigned to global variables.

The two commas surrounding "with legacy facts" are not necessary or should follow "Puppet 8". A comma after "and below" makes more sense.

> When Puppet is run, either via the agent or by running `puppet apply` on the command line, Facter will run with legacy facts disabled in Puppet 8 or enabled in Puppet 7 and below, and the output will be assigned to global variables.

---

:notebook: The reference to the `$facts` array in this sentence,

> These variables can then be accessed in Puppet manifests in two ways – either directly by the name of the fact on a global variable or via the facts array.

May instead be formatted (and passive voice removed):

> These variables are accessed in Puppet manifests in two ways: either directly by the name of the fact on a global variable or via the `$facts` array.

---

The sentence,

> For example, in the following code, the notify resources would access the `kernel` and `os family` variables and print logging messages containing the kernel and os families of the host it was run on:

Refers to the `os.family` fact as `os family` and calls them variables instead of facts. It should be,

> For example, in the following code, the `notify` resources access the `kernel` and `os.family` facts and output messages containing the kernel and OS family of the host it was run on:

---

The subsequent code example does not properly refer to elements of the `$facts` hash, lacking single quoted hash keys as well as the closing brace for the `os.family` fact.

It should be formatted:

```puppet
notify { "This client's kernel is ${facts['kernel']}": }
notify { "This client is a member of the OS family ${facts['os']['family']}": }
```

---

## Page 100

The indentation for the example `factor.conf` is inconsistent.

---

## Page 101

:notebook: In the sentence,

> The cli section sets a log level with a string of (`none`, `trace`, `debug`, `info`, `warn`, `error`, `fatal`) and has three options: `verbose`, `trace`, and `debug`. Each of these three options is enabled or disabled with a `true` or `false` Boolean.

The list of logging levels does not need parentheses and the paragraph can be simplified thus,

> The CLI section sets the log level with a value of `none`, `trace`, `debug`, `info`, `warn`, `error`, or `fatal` and has three Boolean options: `verbose`, `trace`, or `debug`, which are enabled or disabled with either `true` or `false`.

---

## Page 102

The conclusion of the note at the top of the page does not need the word "basis."

---

The sentence,

> In *Chapter 8*, you will learn how external facts can be distributed to clients from modules via the plugin sync process, where facts are added from modules contained in a `facts.d` folder within the module.

Can be simplified by removing ", where facts are added from modules contained."

> In *Chapter 8*, you will learn how external facts can be distributed to clients from modules via the plugin sync process contained in a `facts.d` folder within the module.

---

## Page 103

In the note,

> Puppet can be run as a non-root user on UNIX-based systems, while external facts can be stored in `~/.facter/facts.d/` ...

The use of "while" should be "with." For example, with passive voice removed:

> Running Puppet as a non-root user on UNIX-based systems is possible with external facts stored in `~/.facter/facts.d/`.

---

The YAML-formatted external facts example does not pass `yamllint` due to too many spaces before and--in the case of `Application`--after the colons. It should be formatted:

```yaml
---
Application: exampleapp
Use: Production
Owner: exampleorg
...
```

---

:notebook: JSON-formatted external facts are easier to read when formatted as:

```json
{
  "Application": "exampleapp",
  "Use": "Production",
  "Owner": "exampleorg"
}
```

---

:notebook: The paragraph about Windows line endings could be a Note section and "BOM" should be "byte order mark (BOM)."

---

The YAML-formatted structured facts example has the same problem as the simpler external facts example: too many spaces before (and after) the colons. In addition, the keys `Use` and `Owner` are duplicated, the `Owner` array does not have a colon and its elements are not properly indented.

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

---

## Page 104

In the Bash shell example, the system calls to `pidof` and `ps` need to be surrounded by parentheses, not braces. In addition, the `ps -C` command does not return the percent CPU or memory used.

An alternative for `%cpu` and `%mem` could be:

```bash
#!/bin/bash
echo "exampleapp_pid = $(pidof exampleapp)"
echo "exampleapp_cpu_use = $(ps -p $(pidof exampleapp) -o pcpu | tail -1) %cpu"
echo "exampleapp_memory_use = $(ps -p $(pidof exampleapp) -o pmem | tail -1) %mem"
```

The Windows PowerShell example script has insufficient parentheses. It should be formatted:

```powershell
Write-Output "exampleapp_pid=$((Get-Process explorer).id)"
Write-Output "exampleapp_cpu=$((Get-Process explorer).cpu)"
Write-Output "exampleapp_mem=$((Get-Process explorer).pm)"
```

---

## Page 105

:notebook: The opening paragraph under the "Custom facts" heading can be rewritten for better clarity as,

> Custom facts are Ruby code that sets facts and expand on the core Facter facts. The main advantage of using custom facts over external facts are the built-in mechanisms.
>
> In this section, you will learn how custom facts allow you to access the value of other facts, how you can have multiple weighted resolutions, and how to use `confine` to ensure only certain nodes will attempt to run the fact.

---

:notebook: The second paragraph can be rewritten as,

> It is beyond the scope of this book to dive deeper into the details of Ruby, but we will show its basic structure and some of its core libraries give you enough of a head start to research them further.

---

:notebook: In the Ruby examples that output `exampleapp --version` the full path to the `exampleapp` binary should be provided.

---

There are discrepancies between `exampleapp -version` and `exampleapp --version` throughout pages 105 and 106.

---

## Page 106

In the paragraph that references the  `os.arch` fact, there is a period missing between `os` and `arch` and the variable reference to `arch` is missing the `$` symbol.

It should be,

> It can be useful to place the value of another fact into a variable. The following code puts the `os.arch` fact into the `$arch` variable:

---

## Page 108

The Ruby code examples are not properly indented. They should be formatted as:

```ruby
require 'puppet/util/feature'
Puppet.features.add(:example_app) do
  windows= `powershell '(Get-Command exampleapp).source'`.strip
  linux = `sh -c 'command -v exampleapp'`.strip
  windows.empty? && linux.empty? ? false : true
end
```

And,

```ruby
Facter.add('exampleapp') do
  setcode do
    confine { Puppet.features.example_app? }
```

---

The example that spans pages 108 and 109 lacks proper indendation and has too few `end`s. It should be formatted:

```ruby
Facter.add('exampleapp_version') do
  has_weight 100
  setcode do
    `exampleapp --version`
    Custom facts and external facts 109
  end
  Facter.add('exampleapp_version') do
    has_weight 50
    setcode do
      `grep version /etc/exampleapp/exampleapp.conf | awk '{ print $2 }'`
    end
  end
end
```

---

## Page 110

The first structured fact Ruby example is not properly indented. It should be formatted,

```ruby
Facter.add(:exampleapp, :type => :aggregate) do
  Chunk(:version) do
    `exampleapp –version`
  end
  Chunk(:fullpath) do
    `which exampleapp`
  end
end
```

---

## Page 111

The Ruby example for returning structured facts is not properly indented and is missing two `end`s.

It should be formatted as,

```ruby
Facter.add('exampleapp.version') do
  setcode do
    `exampleapp --version`
  end
  Facter.add('exampleapp.pid') do
    setcode do
      `pidof exampleapp`
    end
  end
end
```

---

## Page 113

:notebook: The sentence that ends the first paragraph under the heading "Statement functions" needs clarification.

> "You cannot add custom or Forge-provided statement functions."

Cannot add them to what?

---

## Page 114

References to 'pa-risc' should be 'PA-RISC.'

---

In the paragraph that begins,

> This differs from the examples this book has used up till now, particularly with the notify resource used in the previous chapter’s examples.

The apostrophe for "chapter's" should be "chapters' to indicate multiple chapters, not a single chapter".

---

## Page 115

:notebook: The second paragraph after the heading, "Comparison and sizing" ends with,

> For example, the following command would return 4 as the length of the string four and 5 as the size of the array:

The reference to 'four' as a string should be quoted.

---

## Page 116

The sentence,

> `max` and `min` are used as prefix functions.

Is innacurate as both are not exclusively prefix functions. This qualifier also disagrees with the subsequent code example. It should be removed and the introductory sentence reworked to either not mention prefix and chain or to mention them both.

The final sentence in the same paragraph does not refer to the variable names as variables. It should be formatted,

> In the following example, the variable `$highest_number` returns 88, while `$lowest_letter` returns 'a':

---

In the paragraph with the following sentence, the references to variables is inconsistent. It should be formatted as,

> In the following examples, the `$empty_array` and `$empty_string` return `true`, while the `$nonempty_string` variable returns `false`:

---

The code example for the `empty()` function has inconsistent spacing around the equal symbols. The use of parentheses for the function is inconsistent.

It should be formatted,

```puppet
$empty_array = [].empty()
$empty_string = empty('')
$nonempty_string = 'not_empty'.empty()
```

---

In the sentence ending the paragraph for the `compare()` function, the word "casing" should be "case."

> For two strings, use a third Boolean argument to check whether the comparison should ignore case.

---

The paragraph for the `compare()` function incorrectly states that the value of `$string_compare` is `1`. The example code actually returns `-1` regardless of the value of the case sensitive boolean option. 'A' (0x41) always comes before 'b' (0x62); as does 'a' (0x61).

A more precise example,

```puppet
$numeric_compare = compare(5, 6)                # -1
$string_compare_neg1 = compare('a', 'A', false) # -1
$string_compare0 = compare('a', 'A', true)      #  0
$string_compare1 = compare('b', 'a', false)     #  1
```

---

In the paragraph,

> `capitalize`, `camelCase`, `downcase`, and `upcase` are all used as prefixes or chained functions to change the capitalization of a string or a set of strings on an iterable, such as an array. `downcase` and `upcase` can also be used on an array. All can be used on a numeric but will simply return the numeric unaffected.

The sentence, "`downcase` and `upcase` can also be used on an array." is redundant and should be removed.

---

"CamelCase" at the beginning of the next paragraph should instead be `camelCase()`.

---

## Page 117

The `capitalize()` code example should have a space after the `=` symbol:

```puppet
$capitals = capitalize(['up', 'miX'])
```

---

The `downcase()` example has a space in the first hash rocket and is missing the closing quotes for both 'Lower' and 'Case2'.

It should be formatted:

```puppet
$downcase = {'lower' => 'case', 'Lower' => 'Case2'}.downcase()
```

---

In the paragraph under the heading "String manipulation",

> The `lstrip`, `rstrip`, and `strip` functions allow spacing to be removed from strings. They are all prefixes or chained functions that are used to remove spaces from a string. `lstrip` removes leading spacing, `rstrip` removes trailing spacing, and `strip` removes both leading and trailing white spacing such as space, tab, newline, and return but not hard space.

The sentence, "They are all prefixes or chained functions that are used to remove spaces from a string." is redundant.

The opening sentence could read,

> The `lstrip()`, `rstrip()`, and `strip()` are all prefix or chain functions that remove whitespace from strings.

In addition, the use of "leading" and "trailing" whitespace for `lstrip()` and `rstrip()`, respectively, should instead refer to whitespace to the left and right of the string. Not all languages lead from the left or trail from the right.

The subsequent code examples reinforce the correct use of left and right.

---

## Page 118

The opening sentence under the "Lambdas" heading uses unecessary plurals for "...arrays or hashes variables." It should be simply, "...array or hash variables."

---

The code example creates a hash variable, `$usersids` then iterates with the `each()` function over the variable `$userids`. There is an extra 's' in the hash declaration, it should be `$userids` to match the iteration.

---

:notebook: In the sentence under the "Templating" heading,

> ... In *Chapter 7*, we will cover templates in full, but the `template` and `epp` functions allow the ERB and EPP formats for templates to be used via the `content` attribute of the `file` resource.

Should be,

> ... While *Chapter 7* covers templates in more detail, know that the `template()` and `epp()` functions allow the use of ERB and EPP formats for templates via the `content` attribute of the `file` resource.

---

## Page 119

:notebook: The `inline_epp()` code example is more readable with additional line breakers:

```puppet
file { '/etc/ntp.conf':
  ensure  => file,
  content => inline_epp(
    $exampleapp_conf_template,
    {
      'port'      => $exampleapp_port,
      'debugging' => $exampleapp_debugging_enabled
    }
  ),
}
```

---

The code example for the `dig()` function should also be formatted for legibility. In addition,the first key, `exampleapp_pids` is missing the 'a' in 'example', the value for the `user` key is not quoted, the `notify` resource does not have a `$` prefix for `exampleapp_proc.dig()`, and the reference to `124` in the `dig()` function is an `Integer` and, therefore, should not be quoted.

It should be formatted,

```puppet
$exampleapp_proc = {
  exampleapp_pids => {
    123 => {
      'state' => 'running',
      'user'  => 'root',
    }
  }
}
notice $exampleapp_proc.dig('exampleapp_pids', 124, 'state')
```

---

## Page 120

The output of the `join()` function within the statement,

> ... would print `[ {London => [ 'bromley', 'brentford' ] }@@Berlin@@Falkirk@@Grangemouth ]`

Is incorrect. The correct output is:

> ... outputs `{"London"=>["bromley", "brentford"]}@@Berlin@@Falkirk@@Grangemouth`

---

:notebook: In the conclusion to the paragraph about the `join()` function and nested hashes,

> ... because the first element of the array is a hash and it won’t be flattened despite it containing a hash:

Can be written to remove the redundant element:

> ... because the first element of the array is a hash it won’t be flattened:

---

The output that concludes the paragraph for the `keys()` and `values()` functions is missing a quote for 'Amsterdam.'

It should be:

> ... while the next two output an array of `['Berlin', 'Amsterdam']`:

---

## Page 122

The claim in the paragraph under the "Arrays and strings" heading that begins,

> The `intersection` function is a chained function ...

Does not match the code example, which uses `intersection()` as a prefix function.

---

The concluding statement from the same paragraph,

> For example, the following code will put the `['both']` array into the `chained_array` variable:

Should be,

> For example, the following code puts the array `['both']` into the `$chained_array` variable:

---

A similar change should be made to the paragraph for the `union()` function. It should be:

> In the following example, the `$union_array` variable will contain the array `['first','second']`:

---

As with the `intersection()` function, the text states that both `union()` and `range()` functions are chain functions then subsequently uses them as prefix functions. In addition, the documentation for `stdlib` does not expressly state that any of the three are exclusively chained functions.

---

The output in the paragraph for the `range()` function uses 'starttrek8', which should be 'startrek8' (one too many 't's).

---

## Page 123

The code example for `start_with()` and `end_with()` do not have an underscore separating the words of the function and use 'starts' and 'ends' rather than 'start' and 'end'.

It should be formatted:

```puppet
$truestart = 'server1234'.start_with('server')
$falseend = 'wales'.end_with('land')
$trueoptions = 'aws104'.start_with['gcp','az','aws']
```

---

The code example under the "Lab" heading references the `os.family` fact as a single element of the `$facts` hash rather than their separate entities. It is also missing spaces surrounding the `else` statement.

It should be formatted,

```puppet
if $facts['os']['family'] == 'windows' {
}
else {
}
```

---

## Page 124

The code example under the "Deferred functions" heading lacks proper indentation and uses double quotes instead of single quotes in the second argument to the `Deferrerd()` function.

It should be formatted,

```puppet
user { 'exampleapp':
  password => Deferred('vault_lookup::lookup', ['exampleapp/password'])
}
```

---

## Page 125

The code example using two `notify` resources has extra whitespace, uses double quotes for the array argument, and is missing the closing brace for the `${deferred}` variable in a string.

It should be formatted,

```puppet
$deferred = Deferred('vault_lookup::lookup', ['exampleapp/message'])

notify { 'this will return the object name':
  message => "Secret message is ${deferred}",
}

notify { 'this will return the message':
  message => $deferred,
}
```

---

## Page 126

:notebook: The use of "dependency hell" at the end of the "Summary" is not a great choice of words. "Circular dependencies" is a better choice for Puppet dependency problems.
