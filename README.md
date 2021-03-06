# SublimeText - InsertDate #

A plugin for Sublime Text 2 that inserts the current date and/or hour according to the format specified and supports named timezones (preferrably using [pytz][pytz] but can interpret the locale's timezone settings if necessary).
It supports multiple selections (regions) and will replace selected text.

For more information about the accepted formatting syntax, see [`datetime.strftime()` behavior][strptime].

## Installation ##

**With [Package Control][pck-ctrl]**: Once installed, bring up the Command Palette (`Command-Shift-P` on OS X, `Ctrl-Shift-P` on Linux/Windows). Select `Package Control: Install Package` and then select `InsertDate` when the list appears. Package Control will automagically keep the plugin up to date with the latest version.

**Without Git**: Download the latest source from [GitHub][github] ([.zip][zipball]) and copy the folder to your Sublime Text "Packages" directory (you might want to rename it to "InsertDate" before).

**With Git**: Clone the repository in a subfolder "InsertDate" in your Sublime Text "Packages" directory:

    git clone git://github.com/FichteFoll/sublimetext-insertdate.git


The "Packages" directory is located at:

* Linux: `~/.config/sublime-text-2/Packages/`
* OS X: `~/Library/Application Support/Sublime Text 2/Packages/`
* Windows: `%APPDATA%/Sublime Text 2/Packages/`

Or enter
```python
sublime.packages_path()
```
into the console (`` Ctrl-` ``).

## Usage ##

For example keymap definitions, see [Default.sublime-keymap][keymap] ([OSX][keymap-osx]).

### Commands ###

**insert_date**

>	*Parameters*

>	- **format** (str) - *Default*: `'%x %X'`
>	  A format string which is used to display the current time. See [`datetime.strftime()` behavior][strptime] for reference.

>	- **prompt** (bool) - *Default*: `False`
>	  If `True` a small popup window will be displayed in which you can specify the format string manually.
>	  The string passed in `format` will be used as default input, `''` otherwise.

>	- **tz_in** (str) - *Default*: `'local'`
>	  Defines in which timezone the current time (read from your system) will be interpreted. Required if you want `%Z` (your timezone's name).
>	  May be one of [these][timezones] values or `'local'`.

>	- **tz_out** (str) - *Default*: `tz_in`
>	  Defines on which timezone the output time should be based	.<br />
>	  May be one of [these][timezones] values or `'local'` (which does not support `%Z` yet, but `%z`).



### Format Examples ###

| Format string            | Parameters                       | Resulting string                   |
|:-------------------------|:---------------------------------|:-----------------------------------|
| `%d/%m/%Y %I:%M %p`      |                                  | 13/05/2012 03:45                   |
| `%d. %b %y`              |                                  | 13. Mai 12                         |
| `%H:%M:%S.%f%z`          |                                  | 15:45:26.598000+0200               |
| `%Y-%m-%dT%H:%M:%S.%f%z` |                                  | 2012-05-13T15:45:26.598000+0200    |
| `iso`                    | `{'tz_out': 'UTC'}`              | 2012-05-13T13:45:26.598000+00:00   |
| `%x %X UTC%z`            | `{'tz_in': 'local'}`             | 13.05.2012 15:45:26 UTC+0200       |
| `%X %Z`                  | `{'tz_in': 'Europe/Berlin'}`     | 15:45:26 CEST                      |
| `%d/%m/%Y %I:%M %Z`      | `{'tz_in': 'America/St_Johns'}`  | 13/05/2012 03:45 NDT               |
| `%x %X %Z (UTC%z)`       | `{'tz_out': 'EST'}`              | 13.05.2012 08:45:26 EST (UTC-0500) |
| `%x %X %Z (UTC%z)`       | `{'tz_out': 'America/New_York'}` | 13.05.2012 09:45:26 EDT (UTC-0400) |

Notes:<br />
`%x` and `%X` are representative for 'Locale’s appropriate time representation'.<br />
`%p` also corresponds to the locale's setting, thus using `%p` e.g. on a German system gives an empty string.


## Libraries ##

- ***[pytz-2012c-py2.6][pytz]*** ([ext. download][pytz-down])<br />
     **pytz** by Stuart Bishop is used for displaying and conversion between timezones. **MIT licence**


## ToDo ##

- Support `%Z` with `tz_in="local"`
- Default (fallback) format string to be configured in settings
- `shift` parameter (`datetime.timedelta(**shift)`)
- `locale` option to modify `%x %X %p` representation?
- Keep history of recently used format strings and display in a quick panel


[github]: https://github.com/FichteFoll/sublimetext-insertdate "Github.com: FichteFoll/sublime-insertdate"
[zipball]: https://github.com/FichteFoll/sublimetext-insertdate/zipball/master
[pck-ctrl]: http://wbond.net/sublime_packages/package_control "Sublime Package Control by wbond"

[pytz]: http://pytz.sourceforge.net/ "pytz - World Timezone Definitions for Python"
[strptime]: http://docs.python.org/py3k/library/datetime.html#strftime-strptime-behavior "Python docs: 7.1.8. strftime() and strptime() Behavior"
[pytz-down]: http://pypi.python.org/pypi/pytz#downloads "pytz : Python Package Index"

[keymap]: https://github.com/FichteFoll/sublimetext-insertdate/blob/master/Default.sublime-keymap "Default.sublime-keymap"
[keymap-osx]: https://github.com/FichteFoll/sublimetext-insertdate/blob/master/Default%20%28OSX%29.sublime-keymap "Default (OSX).sublime-keymap"
[timezones]: https://github.com/FichteFoll/sublimetext-insertdate/blob/c879a70e12fb38c86a893b2be7979b4f7111b342/pytz/__init__.py#L527-L1101 "List of timezones in source"
