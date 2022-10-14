### borrows heavily from https://github.com/StyraInc/rego-style-guide

# Hashicorp Sentinel Style Guide
This style guide provides a series of recommendations and best practices around authoring Hashicorp Sentinel policies. This is a set of guidelines that draws from the collective experience of both our Sentinel team and our capable Sentinel community.


# Writing Sentinel Policies
#### Emphasize Readability

Sentinel policies are declarative. As such, it's a responsibility of the Sentinel runtime to run policies efficiently, rather than the responsibility of policy authors.
Policies should be designed to be understood at a glance rather than for brevity or efficiency.

#### Use `sentinel fmt`

Implementation of unified formatting for Sentinel policies is a general best practice, and made trivial via use of the `sentinel fmt` command (which can be added to CI pipelines). This both makes the code more readable and potentially reduces code review overhead.

### Add comment blocks above your rules

Comment blocks can be added above a given rule to add metadata around its behavior. When the rule is evaluated, this block will be displayed. 

### Use snake case for rule names, variables, and functions

Sentinel imports utilize `snake_case`. Consistent casing makes code more organized and readable.

### Wrap lines for readability

For readability, it is generally a good idea to keep lines short. It can be useful to add newlines between conditions in longer statements.

```
resources = filter tfplan.resource_changes as _, rc {
	rc.type is "resource_name" and
		rc.mode is "managed" and
		rc.change.actions in actions
}
```

# Writing Rules

### Use helper functions and import rules to emphasize policy readability

Storing rules and functions separately allows them to be utilized across multiple policies. Where conditional logic is concerned, it can also make policies significantly more readable.

### Handle undefined

You can use Boolean logic to [safely recover from `undefined`](https://docs.hashicorp.com/sentinel/language/undefined#boolean-logic-and-undefined). `else` expressions are also suitable for this purpose.

# Effective Looping
### Use `contains` or `in` to check whether a given value is present in a list or map. 
This is more readable than equality comparisons to a given `string`, particularly when checking said list or map should NOT contain a value.

### Use `all`  and `any` when appropriate

### Use `maps` rather than `lists` (where possible)
Operating against a `map` is more performant than operating against a `list`. Keys can be semantically connected to the value and this will result in more readable code.


