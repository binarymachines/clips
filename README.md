clips
=====

clips stands for Command LIne Python Scripts: assorted tools to make life easier in the Big Texty.


<b>scpget</b> and <b>scpput</b> are wrappers around (you guessed it) scp. They follow scp's semantics as closely as possible, with the
additional benefit being that they're smart about aliases. So whereas with scp you would say

```bash
scp me@<host.domain.com>:<path/to/file> [localfile]
```

you would issue

```bash
scpget me@<host.domain.com> ...
```

No difference there. But if you have 

```bash
alias a='ssh host.domain.com'
```

in your .bashrc, you can issue

```bash
scpget me@a:<path/to/file/> [localfile]
```


and it all just works. scpput works the same way of course, just in the opposite direction.


<b>mktunnel</b> makes setting up SSH tunnels a bit easier. I often find myself having to jump into a private server through a bastion host.
mktunnel basically wraps ssh *and* lets me use my aliases.


So say your server is saturn.sol.pvt and your bastion host is gateway-server-123.sol.com. You've set up a web stack on saturn
that you want to hit with a browser from your local machine. You also have a couple of aliases in .bashrc like

```bash
alias gate='ssh gateway-server-123.sol.com'
alias s='ssh saturn.sol.pvt'
```

so just issue

```bash
mktunnel 9999 s:80 gate
```

Now your tunnel is up and ready to go; from your browser you can issue the URL

```bash
http://localhost:9999
```

to hit the private host.

<b>spinup</b> is a utility for booting and provisioning ("spinning up") EC2 instances, using Chef as a configuration manager.
Right now it's experimental software, but it does work correctly provided you have the Gremlin library installed (Gremlin is
a curses-based pythonic framework for running menu-based command line programs); issue 'pip install gremlin' to pull it down from PyPi.

Then make sure the file is on your PATH and type spinup at the command line to run it. Spinup will ask a series of questions
regarding your server, then launch an EC2 instance using the Chef knife command. To launch spinup in debug mode (it will
generate but not execute the knife command string), run spinup with the --debug option; to append the generated command string
to an existing file such as a script under construction, run it with the --debug and --append options.








