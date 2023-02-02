# neudist

Not Entirely Unlike a DISplay Tester.

A helper tool (bourne shell script) for calibrating and profiling displays
with Argyll CMS.

Since DisplayCal is no longer in my Linux distro (Debian Sid) on account of
Python 2.7 dependencies that got removed, I wrote this helper script to assist
me in driving Argyll CMS's tools directly.

I am too dumb to remember all of the steps for directly using Argyll, so I
wanted to make a "one-stop-shop" tool that would handle my calibration and
color profiling needs on my (Linux-based) machines, either while I wait for
DisplayCAL to get ported to Python 3. Maybe even permanently.

I share this in the hopes that it will help others. If you need a feature that
Argyll or DisplayCAL exposes which I do not have a way to use, please create
an issue or a pull request and I'll get on it as soon as I can.

Similarly, if I made oversights (I am **certain** that I did), please let me
know about them.

Run the script with `--help` for a full writeup.

If run without any arguments, or run with only one argument (a profile name),
the script will try to calibrate and profile a screen with default Argyll
`dispcal` values (which usually means argyll measures and determines for you).
It will put the results in a directory with the name provided as an argument.

You may have to provide a path to your colorimeter correction files, or use
`--no-correction` if you have a spectrometer. This path can be provided on
the command line, or it can be made the default by editing the script near the
top. I might move this to a configuration file later, if this thing gets
larger.

I have only used this tool three times so far, so be warned. It shouldn't
destroy anything, but I take no responsibility if it does. **Don't run it
as root**, at the very least. Set up udev rules or change permissions for
your colorimeter instead.

Tested so far on a PowerBook G4 and also my x86 (amd64) desktop, where it
is working pretty much on par with DisplayCAL while using far fewer resources.

### Bugs

* Yes.

* Please report bugs as you find them; pull requests are even more appreciated.

* Not my bug, but older Firefox, Seamonkey, and Pale Moon don't like L*A*B
profiles, it seems. So I have made XYZ cLUT + Matrix the default
(`--algorithm X`). For the Argyll default, do `--algorithm l`. New firefox
(tested on 89) seems to handle it alright.

* While it works very nicely for doing calibration, profiling, and profile
creation in one swoop (probably the most common use case), attempting to skip
some steps may not work as nicely as I would like for it to. That's bad
mostly because if some stage of calibrating/profiling fails, you have to start
over from square one or follow the rest of the script manually.

* The aforementioned functionality is currently documented so that I might fix
it some day, but if you want to do something like creating multiple profiles
from a single measurement session you may be better off reading the logs to
find out what arguments to pass to the Argyll CMS command line tools directly.
I also recommend doing this as a way to gain an insight into how display
calibration/profiling actually works.

* Argyll is an extremely powerful set of programs, and what my program exposes
barely scratches the surface of what it can do, even just within the realm of
display calibration/profiling.

* Unfortunately, due to how I chose to implement the script, it may be
challenging for me to fully support doing smaller individual steps. There are
also plenty of places where documentation could be improved or command line
flags could be renamed/added for additional functionality.

* Some paths are hardcoded. It would be wise to search through the script
and see where it is mentioning paths like `/usr/` to make sure you have the
files it is going to look for on your system. The Argyll CMS package puts most
of those files in the right places on Debian and Debian derived systems, but
I can't guarantee it works every time.

* I believe that right now I am implicitly assuming anyone who is calibrating
and profiling their screens is targetting SRGB. This is a clearly bad
assumption. I just don't have any wide gamut screens and haven't been bugged
quite enough about it to fix it. Please bug me if you consider it important,
and it will greatly increase the odds that I will try to do something about it!

