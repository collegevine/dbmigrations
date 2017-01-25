# CV-Specific README

We've fixed `dbmigrations` to version 1.1.1, installable by stack. Simply run `stack install`.

If you get an error about `mysql_config`, you'll need to install `mysql` via homebrew first. It's unfortunate, but necessary. `brew install mysql`.

If you get another error about missing c libs, such as the following:
```
    Configuring mysql-0.1.4...
    setup: Missing dependencies on foreign libraries:
    * Missing C libraries: ssl, crypto
    This problem can usually be solved by installing the system packages that
    provide these libraries (you may need the "-dev" versions). If the libraries
    are already installed but in a non-standard location then you can use the
    flags --extra-include-dirs= and --extra-lib-dirs= to specify where they are.
```

Then you will need to tell stack where to find the local installation of openssl, namely `stack install --extra-include-dirs=/usr/local/opt/openssl/include --extra-lib-dirs=/usr/local/opt/openssl/lib`

You can now check that you have `moo` on your path: `which moo`. You may also have seen a warning like `WARNING: Installation path /Users/mohanzhang/.local/bin not found on the PATH environment variable` in which case you'll need to add the path or simply call `moo` explicitly using its absolute path.

## Running migrations

By convention, look for a file named `moo.cfg` or `moo.cfg.dist` inside the project. Rename this file to `moo-prod.cfg` using the proper environment variables; we typically inline the instructions on how to retrieve the variables. You can repeat this process for `moo-stage.cfg`.

Now you can run moo from within the project using e.g. `~/.local/bin/moo upgrade -c moo-stage.cfg`.
