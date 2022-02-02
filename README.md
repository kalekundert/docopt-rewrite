I want to make a library that's in the same vein as docopt, but with a variety of improvements.  Most of the improvements are in service of these big goals:

- Make more metadata available (e.g. distinguish between default value and value specified by user).  This is particularly important for byoc.
- Easier to reuse options between related scripts.  This is the biggest weakness of the docopt approach, IMO.

With that in mind, here are the specific features I have in mind:

- Two load functions, one that returns a custom data structure with lots of metadata, and another that just returns a simple dictionary.  It may be possible to combine these into one if I'm clever enough about it.

- Make available a parsed representation of the usage text.  This could be used to automatically build shell completion plugins.

- Allow the user to specify a list of docstrings where option descriptions may be taken from.  This is for sharing common options between commands.  Each command must still specify its own usage section, but the long descriptions can be imported from these other strings.  The long descriptions would appear in the same order as specified by the usage section.

- Use module docstring by default.

- Better unit tests, and a real parsing library.  Docopt is pretty buggy.
