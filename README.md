I want to make a library that's in the same vein as docopt, but with a variety of improvements.  Most of the improvements are in service of these big goals:

- Make more metadata available (e.g. distinguish between default value and value specified by user).  This is particularly important for byoc.
- Easier to reuse options between related scripts.  This is the biggest weakness of the docopt approach, IMO.

With that in mind, here are the specific features I have in mind:

- Two load functions, one that returns a custom data structure with lots of metadata, and another that just returns a simple dictionary.  It may be possible to combine these into one if I'm clever enough about it.

- Make available a parsed representation of the usage text.  This could be used to automatically build shell completion plugins.

- Allow the user to specify a list of docstrings where option descriptions may be taken from.  This is for sharing common options between commands.  Each command must still specify its own usage section, but the long descriptions can be imported from these other strings.  The long descriptions would appear in the same order as specified by the usage section.

  - If the same option has multiple long descriptions, only the first will be used.  This allows for overwriting default descriptions with more specific/tailored info.

- Use module docstring by default.

- Better unit tests, and a real parsing library.  Docopt is pretty buggy.

- Support this usage syntax: `foo [-x <y>...]`

  This means that the `-x` option could be followed by any number of values.
  
- Better error messages.  When docopt fails to parse the command-line arguments and prints out the usage text, it gives no hint as to what the problem was.  Even with short command-lines, I can have trouble figuring out the issue.  With long command-lines it's really bad.

- Allow user to specify custom program name, i.e. how much of the beginning of the usage line to ignore.  By default, the first word on the usage line will be taken as the program name.  But sometimes I have scripts that are meant to be run as 'python -m path.to.module', and it'd be nice to support things like that.

- Force the user to include `--help` in the usage text.  Have an argument for what the name of the "help" argument shuold be, then complain if that name isn't in the usage text.
  - That said, the git commands don't explicitly list the `--help` option.
 
A possibly relevant standard to reference: https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap12.html#tag_12_01
