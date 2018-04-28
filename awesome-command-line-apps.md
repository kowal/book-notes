## Build Awesome Command-Line Applications in Ruby

> by David B. Copeland

If you like the notes, go ahead and [buy the book](https://pragprog.com/book/dccar2/build-awesome-command-line-applications-in-ruby-2)!

- Define clean, concise purpose, be simple to use
  - Command Line Interface - the most important thing !
  - Naming: `my_app --global-option [command] --command-option [argument]`
  - Options
    - forms
      - short-form, for CLI, `git -m`
      - long-form, for scripting, `git --message`
    - types
      - switches, `-foo` might go with `--no--foo` as well
      - flags (with arguments), `-f arg` or `--foo=args`
- `"be helpful"`
  - Print help when
    - no arguments or with `-h / --help` switch
    - with command missing arguments
  - Banner
    - Must be short and to the point
    - `$PROGRAM_NAME` global variable can be used
  - Put more detailed description in command-specific help
  - Include default argument values in help
  - Add man pages, - `gem install gem-man ronn`
  - Writing help
    - for new users - help banner + man page - DESCRIPTION, EXAMPLES
    - for regular users - help details
    - for advanced users - man page 
- `"play well with others"`
  - Use proper exit codes
    ```ruby
    require 'english'
    system('git')
    $CHILD_STATUS.exitstatus == 0
    ```
  - Use standard output and error streams
    - `out, err, status = Open3#capture3('command')`
    - use `STDERR.puts('error')`
    - use `$stderr` when you want to reassign stream without warnings, this can be used for test env. For CLI apps it's probably better to leave that the decision for the user and use `STDERR` instead (which always can be assign to `$stderr` variable)
    - always put something to std error when exiting with non-zero status
    - format output to be used by others
      - to be used with sort, grep, etc
      - provide pretty-print option
    - trap signals
  - way to call system functions
    - `backticks`
      - raise errors, returns stdout, blocking
      - You can redirect `STDERR` to `STDOUT` if you want to capture `STDERR`
      - Checking the status of the operation - `$?.success?`
    - `system('command')` - eats errors, returns true/false/nil, blocking
    - `exec`
      - replaces the current process,
      - does not return anything (if success) or fails with `SystemCallError` (if failure)
    - `sh` - calls system under the hood, easy check status `sh %w(xxxxx) { |ok, res| .. }`
    - `popen3` - allows you to interact with stdin, stdout and stderr
    - `popen2e` - merges stdout with stderr
    - `spawn` - fire subshell and returns pid
- `"delight users"`
  - Use short-form names only for common and nondestructive options
  - Short-form options should be mnemonics for the behavior they control
  - Always provide long-form option, and use when scripting your app
  - Long-form options should be as clear as possible
  - For command suites, use abbrevs/mnemonics for common commands
  - Config files location - by default  `~/.my_app` (hidden)
  - Name file uniquely to avoid collisions (add timestamps)
  - Accept std input stream
  - Chose proper output type based on its destination `STDOUT.tty?`
- `"make configuration easy"`
  - Create external YAML config file which can contain default values for app / commands
