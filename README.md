# legolas

Command line tool to manipulate ELF and other binary & executable files for
embedded systems.  For example legolas allows you to query the contents of
an ELF file using SQL (structured query language) syntax.  You can do simple
queries such as listing all of the symbols:

    legolas elfquery <file> "SELECT * FROM symbols"

Or more advanced queries like listing the contents of RAM in increasing size:

    legolas elfquery <file> "SELECT TO_HEX(Value, 8) AS Value, Size, Section, Name FROM symbols WHERE Section = ".bss" AND Size > 0 ORDER BY Size ASC"

Internally legolas uses an in-memory SQLite database to hold ELF metadata so
the full power of SQLite database queries are available to you!

## Installation

To install clone this repository, open a command line terminal, and navigate
to the cloned directory to run the following command:

    sudo python setup.py install

Note on Windows the sudo command is omitted.

Alternatively to install using the setuptools develop mode (good for changing
the code and testing it), run:

    sudo python setup.py develop

Once installed the `legolas` command line tool will be available to use (assuming
Python is in your system path).  Run `legolas --help` for a list of available
commands and options.

To uninstall use the pip tool:

    sudo pip uninstall Adafruit_Legolas

## Available Commands

Legolas is composed of subcommands that can perform useful actions.  To see a list
of all available commands run `legolas --help`.  To see the usage for a specific
command run it with `--help` like `legolas elfquery --help` to see help on the
elfquery command.

The following commands are available:

-   hexmerge - Merge a collection of Intel format .hex files into a single file.

-   elfquery - Query the contents of an ELF binary file using SQL (structured query language).

## Adding Commands

To add new commands to legolas look inside the `Adafruit_Legolas/commands`
folder.  Each file will be loaded and any function that has the `@main.command()`
decorator will be available as a subcommand.  The tool makes heavy use of the
[Click framework](http://click.pocoo.org/4/) as its command line infrastructure.
See the `hexmerge.py` command file and the comments within for some guidance on
how to add parameters and use Click.
