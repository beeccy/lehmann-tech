# Basic terminal shortcuts

Based on an interactive miniseries at work. Meant for zsh, but mostly works for bash too.

The format isn't fully defined, but I try to include one major change/plugin and four tiny things per week.

## Week 1: Avoid repetition

Week 1 is all about not typing out the same command multiple times.

### `!$`

`!$` refers to the __last__ token from the previous command. Here's how to _not_ use it:

```zsh
grep "a needle" ./some-file.txt
vim ./some-file.txt
```

Here's a better way:

```zsh
grep "a needle" ./some-file.txt
vim !$
```

`!$` gets expanded to the last token in the previous command, rendering the exact same command with less typing.

### `!:2`

Closesly related to `!$`, `!:2` refers to the token at index 2 (i.e., the third token because zero-indexing) in the previous command.

Reusing the example, `grep "a needle" ./some-file.txt` contains the following three tokens (from zsh's perspective):

0. `grep`
1. `"a needle"`
2. `./some-file.txt`

Here, `!:2` refers to the token at index 2: `./some-file.txt`. Therefore, we can achieve our goal as such:

```zsh
grep "a needle" ./some-file.txt
vim !:2
```

Obviously, index-based substitution is more flexible than `!$`. If you find that your `grep` command takes too long and would like to run the same command with something faster like [ripgrep](https://github.com/BurntSushi/ripgrep) instead, you can do:

```zsh
grep "a needle" ./some-file.txt
rg !:1 !:2
```

Or, combine with `!$` to make it even shorter:

```zsh
grep "a needle" ./some-file.txt
rg !:1 !$
```