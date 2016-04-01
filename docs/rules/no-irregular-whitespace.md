---
title: Rule no-irregular-whitespace
layout: doc
translator: molee1905
proofreader: molee1905
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# No irregular whitespace (no-irregular-whitespace)

# 禁止不规则的空白 (no-irregular-whitespace)

Invalid or irregular whitespace causes issues with ECMAScript 5 parsers and also makes code harder to debug in a similar nature to mixed tabs and spaces.

无效的或不规则的空白导致 ECMAScript 5 解析问题，也会使代码更难调试，类似于混合 tab 和空格的情况。

Various whitespace characters can be inputted by programmers by mistake for example from copying or keyboard shortcuts. Pressing Alt + Space on OS X adds in a non breaking space character for example.

各种空白字符是由程序员误输入的，比如拷贝或键盘快捷键。例如，在OS X系统按下 Alt + Space，增加了一个不间断空格。

Known issues these spaces cause:

这些空格引起的已知的问题:

* Zero Width Space

* 零宽度空格

    * Is NOT considered a separator for tokens and is often parsed as an `Unexpected token ILLEGAL`

    * 不被认为是分隔符，经常被解析为`Unexpected token ILLEGAL`

    * Is NOT shown in modern browsers making code repository software expected to resolve the visualisation

    * 不在现代浏览器中显示，期待使用代码存储软件解决其可视化问题。

* Line Separator

* 行分隔符

    * Is NOT a valid character within JSON which would cause parse errors

    * 在JSON中不是一个有效的字符，会引起解析错误

## Rule Details

This rule is aimed at catching invalid whitespace that is not a normal tab and space. Some of these characters may cause issues in modern browsers and others will be a debugging issue to spot.

该规则旨在捕获无效的不是正常的tab和空格的空白。这些字符有的会在现代浏览器中引发问题，其它的会引起调试问题。

With this rule enabled the following characters will cause warnings outside of strings and comments:

启用了此规则，以下字符将会在字符串和注释之外引起警告：

    \u000B - Line Tabulation (\v) - <VT>
    \u000C - Form Feed (\f) - <FF>
    \u00A0 - No-Break Space - <NBSP>
    \u0085 - Next Line
    \u1680 - Ogham Space Mark
    \u180E - Mongolian Vowel Separator - <MVS>
    \ufeff - Zero Width No-Break Space - <BOM>
    \u2000 - En Quad
    \u2001 - Em Quad
    \u2002 - En Space - <ENSP>
    \u2003 - Em Space - <EMSP>
    \u2004 - Tree-Per-Em
    \u2005 - Four-Per-Em
    \u2006 - Six-Per-Em
    \u2007 - Figure Space
    \u2008 - Punctuation Space - <PUNCSP>
    \u2009 - Thin Space
    \u200A - Hair Space
    \u200B - Zero Width Space - <ZWSP>
    \u2028 - Line Separator
    \u2029 - Paragraph Separator
    \u202F - Narrow No-Break Space
    \u205f - Medium Mathematical Space
    \u3000 - Ideographic Space

Examples of **incorrect** code for this rule:

**错误**代码示例：

```js
/*eslint no-irregular-whitespace: 2*/

function thing() /*<NBSP>*/{
  return 'test';
}

function thing( /*<NBSP>*/){
  return 'test';
}

function thing /*<NBSP>*/(){
  return 'test';
}

function thing᠎/*<MVS>*/(){
  return 'test';
}

function thing() {
  return 'test'; /*<ENSP>*/
}

function thing() {
  return 'test'; /*<NBSP>*/
}
```

Examples of **correct** code for this rule:

**正确**代码示例：

```js
/*eslint no-irregular-whitespace: 2*/

function thing() {
  return ' <NBSP>thing';
}

function thing() {
  return '​<ZWSP>thing';
}

function thing() {
  return 'th <NBSP>ing';
}

// Description<NBSP>: some descriptive text

/*
Description<NBSP>: some descriptive text
*/
```

## Options

The `no-irregular-whitespace` rule has no required option and has one optional one that needs to be passed in a single options object:

该规则没有必选项，只有一个可选项是个对象。

* **skipComments** *(default: `false`)*: whether to ignore irregular whitespace within comments (`true`) or whether to check for them in there, too (`false`).

* **skipComments** *(默认: `false`)*: 是否忽略注释中不规则的空格(`true`) 或 非法对它们进行检查 (`false`)

For example, to specify that you want to skip checking for irregular whitespace within comments, use the following configuration:

例如，你想跳过对注释中的不规则的空格的检查，使用下面的配置进行：

```json
"no-irregular-whitespace": [2, { "skipComments": true }]
```

## When Not To Use It

If you decide that you wish to use whitespace other than tabs and spaces outside of strings in your application.

如果你想在你的应用中使用 tab 和空格之外的空白，可以关闭此规则。

## Further Reading

* [ECMA whitespace](https://es5.github.io/#x7.2 \xA0)
* [JSON whitespace issues](http://timelessrepo.com/json-isnt-a-javascript-subset)

## Version

This rule was introduced in ESLint 0.9.0.

该规则在 ESLint 0.9.0 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-irregular-whitespace.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-irregular-whitespace.md)