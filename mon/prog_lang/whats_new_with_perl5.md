# ATO19: Old Dogs & New Tricks: What’s New with Perl5 This CenturyO

*John Anderson*

https://allthingsopen.org/talk/old-dogs-new-tricks-whats-new-with-perl5-this-century/

There is a signicant difference between how the perl community thinks perl works, and how everyone else thinks it works

Perl 5.6 was released in 2001, the current release is 5.30.

What happened in those 19 years
* Between 2002 and 2007, perl almost died
* Since then, it's grown a regular release cycle (roughly once per year, around May)
* The BDFP of Perl5 is the Pumpking (currently SawyerX)
* modernperlbooks.com
* Many language improvements
    * Unicode support

Perl background
* falsey values: 0, '', (), and `undef`
* everything else is truthy
* `undef` is undefine-edness, everything else is defined
* boolean operators look at truthiness, but often the only invalid value is `undef`
* This leads to using `if ( undefined ( $this ) ) { ...` a lot
    * The more ideomatic way is `$value = defined($this) ? $this : 'default';`
    * Now there is a defined-or operator, so the above is now ritten `$value = $this // 'default';`
    * You can also combine with assignment, like `$this //= 'default';` (only changes value if it's undefined)
        * Similar to `$this ||= 'default'`

Regular expression refinements
* Old school: `my $copy = $orig;`, `$copy ~= s/swap/stuff/;` or `(my $copy = $orig) =~ s/swap/stuff/;`, but this is somewhat confusing
* Starting with 5.14: `my $copy = $orig =~ s/swap/stuff/r;` (return the modified value, rather than modifying `$orig`)

Subroutine signatures (the biggest feature this decade)
* No more unpacking `@_`.
* No you can do stuff like `sub add ($one, $two) { ...`
* Supports validation and default values

Some improvements are actually removals...
* Assigning non-zero values to `$[` is fatal
    * This used to be a special value you could assign to to change what the initial index of an array is (in case you want 1 indexing... or 26 indexing... or whatever)
    * Someone thought this was a good idea at some point
    * As of 5.30, any value other than 0 will produce a fatal error

New tools...
* "system" perl (the perl that ships with your OS, i.e. `/usr/bin/perl`)
    * just say no
    * your OS probably has dependancies on Perl to make things work, you probably don't want to be coupled to the OS release pace
* One such tool is [perlbrew](http://perlbrew.pl)
* `plenv` is newer
    * Less magic messing with `$PATH`
    * Can "pin" perl globally, per-shell, or per-directory
* You want to do this because...
    * Solves vendor perl lockin issues
    * Install multiple perls in your home directory (or elsewhere)
    * Trivially switch between versions
    * Install modules without special permissions
    * Easy to stay up to date with perl development

Speaking of installing...
* There are new tools to make it easier to install and manage modules
* `local::lib`
    * installs your own copies of modules
    * in your `$HOME`
    * can also install per-project modules
    * integrates with other tools
    * good docs apparantly
* cpanminus (`cpanm`)
    * better logging
* carton
    * bundler/packagelock, but for perl
* pinto
    * lets you run a "private CPAN"
    * good for use within your organization
    
New CPAN website
* metacpan.org
* integrates and visualizes a lot of module information
* fully open source

`JSON::MaybeXS`
* Perl has many JSON libraries, this one automatically picks the best one you have available on your system

Moose / Moo
* Useful if you want to do OO stuff
* Adds metaprogramming capabilities

CGI.pm is gone
* No longer part of Perl core, but can still be installed from CPAN
* The new standard for perl web development is plack

Speaking of Perl website...
* CPANTS - linting of modules uploaded to CPAN
    * Handy for getting a feel for th elevel of quality of other people's code
    * metacpan links to this automatically
* cpantesters
    * aggregates results from CPAN reporter
    * crowdsourcing to see what OS and perl versions cause failures
    
Speaking of Perl community...
* Perl people are nice 
* Perlmongers
* Perl Weekly newsletter

Questions
* planned features you're excited about?
    * method signatures
* what problem domain is modern perl suitable for?
    * things involving text
    * probably not web programming anymore
    * interfacing with business stuff (munging Excel)
        * i.e. ETL
        * Perl is faster than other interpreted languages for this
* why Moose and Moo and not Mouse or Dot?
    * not familiar with Dot
    * Mouse is deprecated
T
