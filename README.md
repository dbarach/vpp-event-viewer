# vpp-event-viewer

This repo contains a vpp live data event viewer plugin x86_64 Debian
package. Also included: a standalone ubuntu-20.04 binary.The plugin
should work with vpp master/latest images built on or after 12/1/2020,
and eventually with vpp 21.01 (or later) production images.

## Installation

Install vpp Debian packages corresponding to vpp itself, vppinfra, and
so on. The Debian package in this repo has the following dependencies:

```text
    Depends: vpp (>= 21.01), libatk1.0-0 (>= 1.12.4), libc6 (>= 2.3.2),
    libcairo-gobject2 (>= 1.10.0), libcairo2 (>= 1.10.0),
     libgdk-pixbuf2.0-0 (>= 2.22.0), libglib2.0-0 (>= 2.31.18), libgtk-3-0
      (>= 3.21.4), libharfbuzz0b (>= 0.6.0), libpango-1.0-0 (>= 1.14.0),
       libpangocairo-1.0-0 (>= 1.14.0)
```

## Invocation

To start the live viewer, start vpp and use the following
debug CLI:

```text
    vpp# event-logger viewer
       or
    vpp# eve v
```

The vpp event viewer plugin should start, and pop up a window which looks
a lot like this:

<img src="images/plugin.png" >

If that works, great! The live event viewer plugin has been
installed. If not, see if the plugin loaded:

```text
    vpp# show plugin
    <snip>
    40. g2_plugin.so v0.1 G2 Live Viewer plugin
```

Most likely, the plugin will have refused to load for one reason or
another. The "show log" debug CLI should give some clue about what
might have happened. Worst-case, run "/usr/bin/vpp unix interactive" and
watch for undefined symbol complaints concerning the "g2" plugin.

Undefined symbols are the most common reason that a plugin will refuse
to load. If that happens, it's likely that the installed version of vpp
is too old. Update the workspace from master/latest and try again.

## G2 Standalone Viewer

The standalone g2 viewer g2-standalone-ubuntu-20-04 is identical to
the plugin viewer, except that it does not support shared-memory
access to the vpp event log.

After installing the listed dependencies, run the viewer:

```text
   $ g2-standalone-ubuntu-20-04 [file <filename>]
```

## Using the GUI

Here is an annotated G2 viewer screenshot, corresponding to a test pattern.

<img src="images/stand2.png" >

The viewer has two main scrollbars: the horizontal axis scrollbar
shifts the main drawing area in time; the vertical axis changes the
set of visible process traces.  The zoomin / zoomout operators change
the time scale.

The event selector menu changes the set of displayed events.  Using
these tools -- and some patience -- you can understand a given event
log.
