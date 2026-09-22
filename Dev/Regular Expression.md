
global
case-sensitive

Regular Expression (Regex)
-> more powerful, general text matching

Glob Pattern -> matches file paths (`*` does not cross `/`, `**` does)
Regex -> matches any text, far more expressive
both show up in shell and in code (grep/sed use regex, .gitignore uses glob)

Flags
`g` global, `i` case-insensitive, `m` multiline (`^ $` per line), `s` dotall (`.` matches newline)

Character
`.` any char, `\d` digit, `\w` word `[A-Za-z0-9_]`, `\s` whitespace
`[abc]` any of, `[^abc]` none of, `[a-z]` range

Quantifier
`*` 0+, `+` 1+, `?` 0 or 1, `{n,m}` n to m
greedy by default, add `?` for lazy -> `*?` `+?`

Anchor
`^` start, `$` end, `\b` word boundary

Group
`( )` capture, `(?: )` non-capture, `(?<name> )` named
`(?= )` lookahead, `(?<= )` lookbehind