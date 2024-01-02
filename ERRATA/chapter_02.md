# Chapter 2

## Page 20

The bullet point:

* A Linux environment using package managers such as apt for Ubuntu or RHEL-based using Yum.

Should instead be:

* A Linux environment using package managers such as apt/apt-get for Debian based distributions or yum/dnf for Red Hat based distributions.

The final bullet point for Visual Studio Code extensions references an application unrelated to VSCode: `pecdm`. The bullet point should be shifted left to align with "The GitHub CLI" etc.

---

## Page 24

"Augeas" is misspelled in the sentence:

> "Augeuas is very advanced but often over-complicated ..."

---

:notebook: (pages 24-25) The ending of the following sentence lacks a proper subject for what to develop and what to integrate with,

> One of the greatest issues with early Puppet development was the lack of a consensus around how to develop and a lack of integration.

---

The sentence,

> This is certainly not the only way to develop Puppet code, and your organization might require the usage of different tools deponding on the environment.

can be written,

> This is certainly not the only way to develop Puppet code and your organization might require using different tools, depending on the environment.

---

The claim that PDK will be covered "in full" in chapter 8 is misleading as PDK is not covered "in full" in that chapter.

---

Vim is referenced twice, once as 'Vim' and, in the same sentence, as 'VIM.' 'Vim' is correct as it is not an acronym.

---

The sentence ending,

> ... to avoid paying for unecessary virtual machine running time costs on Azure.

can be simplified (and the typo "unecessary" corrected) to,

> ... to avoid paying for unnecessary virtual machine time on Azure.

---

:notebook: References to 'Yum' or 'yum' should be replaced with 'dnf' as Red Hat Enterprise Linux 8+ (and related distributions) use 'dnf' by default. This is also true of the package provider for these distributions.

---

## Page 29

The code example has one typo:

* Line 1: `mkdir ~workspace/pecdm` should instead be `mkdir -p ~workspace/pecdm`

---

:notebook: `~workspace` should be `~/workspace`. Example: `mkdir -p ~/workspace/pecdm`

---

## Page 31

This sentence needs a space after the first comma:

> Puppet has its own learning site (<https://training.puppet.com/learn>),this ...

It should be:

> Puppet has its own learning site (<https://training.puppet.com/learn>), this ...

---

The sentence,

> Puppet's support knowledge base was made public in April 2022, ...

should be a new paragraph.

---

The sentence,

> Puppet previously run two, ... which had to be paid for and lasted 3 ...

Should instead be,

> Puppet previously ran two, ... which had to be paid for and lasted three ...

---

In the paragraph that begins, "The key difference is that" the two words "self paced" should be hyphenated as "self-paced"

---

:notebook: The paragraph beginning,

> This section is not supposed to be an exhaustive ...

Can be simplified to,

> This section is not an exhaustive ...
