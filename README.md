# ember-angle-brackets-codemod

[![Build Status](https://travis-ci.org/rajasegar/ember-angle-brackets-codemod.svg?branch=master)](https://travis-ci.org/rajasegar/ember-angle-brackets-codemod) 
[![Coverage Status](https://coveralls.io/repos/github/rajasegar/ember-angle-brackets-codemod/badge.svg?branch=master)](https://coveralls.io/github/rajasegar/ember-angle-brackets-codemod?branch=master)
[![npm version](http://img.shields.io/npm/v/ember-angle-brackets-codemod.svg?style=flat)](https://npmjs.org/package/ember-angle-brackets-codemod "View this project on npm")
[![dependencies Status](https://david-dm.org/rajasegar/ember-angle-brackets-codemod/status.svg)](https://david-dm.org/rajasegar/ember-angle-brackets-codemod)
[![devDependencies Status](https://david-dm.org/rajasegar/ember-angle-brackets-codemod/dev-status.svg)](https://david-dm.org/rajasegar/ember-angle-brackets-codemod?type=dev)

A [jscodeshift](https://github.com/facebook/jscodeshift) Codemod to convert curly braces syntax to angle brackets syntax for templates
in an Ember.js app

Refer to this [RFC](https://github.com/emberjs/rfcs/blob/master/text/0311-angle-bracket-invocation.md) for more details on Angle brackets invocation syntax.

## Usage 

**WARNING**: `jscodeshift`, and thus this codemod, **edits your files in place**.
It does not make a copy. Make sure your code is checked into a source control
repository like Git and that you have no outstanding changes to commit before
running this tool.

```sh
$ cd my-ember-app-or-addon
$ npx ember-angle-brackets-codemod angle-brackets app/templates
```

## From
```hbs
{{site-header user=this.user class=(if this.user.isAdmin "admin")}}

{{#super-select selected=this.user.country as |s|}}
  {{#each this.availableCountries as |country|}}
    {{#s.option value=country}}{{country.name}}{{/s.option}}
  {{/each}}
{{/super-select}}
```

## To
```hbs
<SiteHeader @user={{this.user}} class={{if this.user.isAdmin "admin"}} />
<SuperSelect @selected={{this.user.country}} as |s|>
  {{#each this.availableCountries as |country|}}
    <s.option @value={{country}}>
      {{country.name}}
    </s.option>
  {{/each}}
</SuperSelect>
```

## AST Explorer playground

1. Go to the [AST Explorer](https://astexplorer.net/#/gist/b128d5545d7ccc52400b922f3b5010b4/571266d8c29cb8eb1bd5730c0c388526081cce46)
2. Paste your curly brace syntax code in the top left corner window (Source)
3. You will get the converted angle bracket syntax in the bottom right corner window (Transform Output)


## Known issues
- No formatting preserved
- Block params need to be tweaked

## Things to do
- Need to add more html attributes

## References:
 - https://github.com/glimmerjs/glimmer-vm/issues/685
 - https://github.com/q2ebanking/ember-template-rewrite
 - https://github.com/ember-template-lint/ember-template-recast
