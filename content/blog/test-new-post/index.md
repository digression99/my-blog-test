# ch 11 - macros

![Test image](./IMG_5113.jpg)

`youtube: https://www.youtube.com/watch?v=2Xc9gXyf2G4`

## intro

- can record any number of keystrokes into registers.
- can append others macros into existing macros.
- can edit the sequence of macro.

## [tip 65] record and execute a macro

- `q{register}` to begin recording.
- if you want to check the saved macros, `:reg {reg}`
  - `^[` is for escape key.
- `@{reg}` to execute the macro.
- `@@` to repeat the macro that was invoked most recently.

## [tip 66] normalize, strike, abort

### rules

- the golden rule - when recording a macro, ensure that every command is repeatable.
  - make sure your cursor is positioned
- prefer word-wise motion to character-wise motion.
  - `0e` will always lead to the end of the character of the first word in a line.
  - it doesn't matter how many characters are inside that word.
- navigate by search
- use text objects

### abort when a motion fails

- vim aborts the rest of the macro when motion fails.

---

- we can do `10@a` to repeat macro in register a 10 times.
  - macro will abort anyway when the motion fails. so you don't have to care for the count. - do `10000@a`

## [tip 67] play back with a count

- dot command cannot be executed with count.
  - record a cheap one-off macro and play it back with a count.
- `;` - repeat the last `f` search.
- to repeat simple task - `qq;.q` , then `11@q`
- challenge
  - `x = "("+a+","+b+","+c+","+d+","e+")";`
  - to `x = "(" + a + "," + b + "," + c + "," + d + ","e + ")";`

## [tip 68] repeat a change on contiguous lines

- you can repeat a macro in multiple lines with some technique.
- normalizing - `0` to position your cursor at the start of the line.
  - when searching with `f`, it's safe and repeatable to use normalizing cursor position.
- if you repeat the macro, it will stop at the line that is not suffice to execute the macro.
  - how can you handle this?

## execute macro in parallel

- record execute only for the one line
- `VG` for the entire lines (or lines that you want to apply macro)
- `:'>,'>normal @a` to execute macro for each lines.
- in `vsc`, normal command does not work.
  - we only can work with macro in series.

## [tip 69] append commands to a macro

- press `qA` to append our keystrokes to register a.

## [tip 70] act upon a collection of files

- need a bit of setup

  set nocompatible
  filetype plugin indent on
  set hidden
  if has("autocmd")
  autocmd FileType ruby setlocal ts=2 sts=2 sw=2 expandtab
  endif

- `:cd {file_path}` - go to that file path.
  - `:args *.rb` - buffers all files ending with `.rb`
  - `:args` - list all files buffered with args command.
- navigate through files
  - `:prev` - to prev file
  - `:next` - to next file
  - you can check what files you are watching with `:args`

---

- `>G` - indent one depth to the rest of the file.

---

- `:argdo` - execute Ex command once for each buffer in the argument list.
  - This will have side effects in the first file, that we just edited.
  - run `:edit!` to make the file in the original state.
  - if you already typed `:w`, this will not work.

### running in series

- you can execute the macro in series by moving to next buffer manually.
- commands
  - `qA`
  - `:next`
  - `q`
  - `22@a`

---

- to save all the files
  - `:argdo write` - save all the files in the argument list
  - `:wall` - save all the files in the buffer list. different from `argdo`
  - `:wnext` - equivalent to running `:write` followed by `:next`
- using tab
  - put all the files inside arg list to tab - `:taball`
  - go to the right tab - `gt`
  -

```javascript
const func = () => {
  console.log("This is test code for line highlighting in gatsbyjs")
}

const func = () => {
  console.log("This is test code for line highlighting in gatsbyjs")
}

const func = () => {
  console.log("This is test code for line highlighting in gatsbyjs")
}
```
