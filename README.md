# RegExHotstrings

Provides RegEx in hotstring triggering like normal hotstring.

Use <kbd>Space</kbd>, <kbd>Tab</kbd> or <kbd>Enter</kbd> to trigger RegExHotstring.

## Usage

```ahk
RegExHotstring(String, CallBack, Options, OnOffToggle, Params*)
```

- String:
  - [RegEx string](https://www.autohotkey.com/docs/v2/misc/RegEx-QuickRef.htm)
- CallBack:
  - calls function with [RegExMatchInfo](https://www.autohotkey.com/docs/v2/lib/RegExMatch.htm#MatchObject) as argument and clear string that triggers it
  - RegExReplace string, works like [RegExReplace](https://www.autohotkey.com/docs/v2/lib/RegExReplace.htm)
- Options:

  A string of zero or more of the following options (in any order, with optional spaces in between)

  Use the following options follow by a zero to turn them off:

  - `*` (asterisk): An ending character (e.g. Space, Tab, or Enter) is not required to trigger the hotstring.

  - `?` (question mark): The hotstring will be triggered even when it is inside another word;
  that is, when the character typed immediately before it is alphanumeric.

  - `B0` (B followed by a zero): Automatic backspacing is not done to erase the abbreviation you type.
  Use a plain B to turn backspacing back on after it was previously turned off.

  - `C`: Case sensitive: When you type an abbreviation, it must exactly match the case defined in the script.

  - `O`: Omit the ending character of auto-replace hotstrings when the replacement is produced.

  - `T`: Use SendText instead of SendInput to send the replacement string.
  Only works when CallBack is a string.
- OnOffToggle

  One of the following values:

  - On or 1 (true): Enables the hotstring.

  - Off or 0 (false): Disables the hotstring.

  - Toggle or -1: Sets the hotstring to the opposite state (enabled or disabled).
- Params:

  additional params pass to CallBack, check [Variadic functions](https://www.autohotkey.com/docs/v2/Functions.htm#Variadic) and [Variadic function calls](https://www.autohotkey.com/docs/v2/Functions.htm#VariadicCall), only works when CallBack is a function.

## Demo

![Demo.gif](demo.gif)

## FAQ

### How to trigger regular hotstring in the same script?

Set `SendLevel` higher than `#InputLevel` (default is `0`), and set `RegHook.MinSendLevel` higher than `SendLevel` to avoid triggering `InputHook` recursively.

```ahk
#Include RegExHotstring.ahk

::btw::by the way

RegHook.MinSendLevel := 2
SendLevel(1)
RegExHotstring(...)
```

> [!IMPORTANT]
> Only last `SendLevel` takes effect.

## Limitations

- incompatible with `#IfWin` or `#HotIf`
- unable to match white space characters.
