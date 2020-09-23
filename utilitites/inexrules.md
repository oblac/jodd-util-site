# InExRules

It's a common practice to set some include and exclude rules to filter some resources. 

This small rule engine is implemented in `InExRules` class. This rule engine may work in one of the two following modes:

* **blacklist** mode \(default\) - any input is included, and you specify

  what to exclude;

* **whitelist** mode - any input is excluded, and you specify

  what to include.

The order of execution of explicit include/exclude rules depends on the mode.

{% hint style="warning" %}
The rules 'opposite' to the rule engine mode are always executed first! Corresponding rules of the same group \(include or exclude\) are executed as they are defined.
{% endhint %}

For example, if rule engine is in blacklist mode, engine first executes exclude rules and then include rules. When executing one of these groups, all corresponding rules are executed as defined. This way you can filter out any combination you need.

I am sure you are totally puzzled with above definitions:\) Let's see rules in action, everything will be much clearer!

### Rules

When created, rules engine can be fill up with the various include/exclude rules. For example, we can have something like this:

```java
InExRules inExRules = ... // we get the engine instance

inExRules.include("shelf.book.*");
inExRules.exclude("shelf.book.page.1");
```

What we set here are two rules: one for defining what will be included and one for what is going to be excluded. In this example, rules are simple strings, but this does not have to be the case, as we gonna see later.

After setting the rule, our engine is set and we can start matching input resources. In our trivial example, resources are again strings, so we can write something like:

```java
inExRules.match("shelf.book.page.1");
inExRules.match("shelf.book");
inExRules.match("shelf.book.page.34");
```

### Order of execution

Above two rules are bit vague. In one rule, we said we want to include all pages, and then we are excluding one page. Which rule is applied first?

Look again what we said on the very beginning. The order of execution depends on current mode. So here is the logic behinds the rule engine in this case:

* By default, engine is created in **blacklist** mode
* Therefore, everything is _included_.
* First check the _opposite_ rules, the _excluded_ group.
* We have just one _excludes_ rule \(`shelf.book.page.1`\).

If we stop now, then the rule engine would be set to include all book pages except the page 1. But we have more rules:

* After checking the _opposite_ group, go with the _included_ group.
* We have one _includes_ rule \(`shelf.book.*`\).

We just overwrite the exclude rule! Meaning, we didn't excluded anything!

### Changing the mode

Obviously, this is not what we wanted. We have to change the initial mode of the rule engine.

then the rule engine logic goes like this

* Engine is started in _whitelist_ mode
* Therefore, everything is _excluded_.
* First check the _opposite_ rules, the _included_ group.
* We have one _includes_ rule \(`shelf.book.*`\).
* After checking the _opposite_ group, go with the _excluded_ group.
* We have just one _excludes_ rule \(`shelf.book.page.1`\).

This time, rules are set like we wanted: the whole book is included except the page 1.

