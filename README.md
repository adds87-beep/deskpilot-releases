# DeskPilot

A menu bar app for a Mac that moves between desks. It keeps the Dock on one screen, and it
remembers where every window and every Space belongs at each desk so it can put them back.

Download the current build from the Releases page. Open the disk image, drag DeskPilot to
Applications, and launch it from there. It is signed and notarised, so macOS opens it
without a warning.

**The full guide**, covering setup, every menu item and setting, what a run does and what
the summary means: **[DeskPilot Guide](https://adds87-beep.github.io/deskpilot-releases/guide.html)**.

## Getting started

On first launch DeskPilot asks for **Accessibility** permission. It is required: moving
other apps' windows and dragging Spaces is done through macOS's Accessibility interface,
and nothing works without it. Grant it in System Settings, Privacy & Security,
Accessibility. If it is listed there and switched on but DeskPilot still says it is not
granted, remove it from the list with the minus button and add it again; macOS ties the
permission to the exact copy of the app that asked.

DeskPilot lives in the menu bar. There is no Dock icon and no window until you open
Settings. It does nothing at all until you tick something.

## Keeping the Dock on one screen

Settings, Dock: tick **Lock the Dock to one display**. macOS moves the Dock to whichever
screen your pointer last pushed against the bottom of. DeskPilot holds the pointer a couple
of points clear of the bottom edge of every other screen, so the Dock is never called
there. "Main display" follows whichever screen has the menu bar, so it works at any desk.

## Saving and applying a layout

**Save Current Layout…** in the menu records, for the set of screens attached right now:
every window's screen, position and size, which Space it is on, the left-to-right order of
Spaces on each screen, and which Space each screen was showing. Your screens flick through
their Spaces for a few seconds while it looks. When saving you choose which apps the layout
may move; unticked apps are never touched.

A layout is offered in the menu only when that same set of screens is attached, so a
laptop-only layout never appears at the desk. **Apply** puts everything back: windows to
their place, Spaces to their screen in your order. Moving a Space between screens has no
programming interface, so it is done by driving Mission Control, which opens briefly and
drags the thumbnails the way you would.

Every run shows a panel with a five second countdown before anything is touched. **Stop**
on the panel, or **Command-Shift-Escape**, stops it at once.

Settings, General: **Detect my desk and apply its layout automatically** applies a saved
layout when the attached screens change to a set you have saved, and never for a set you
have not.

## What is stored

Everything is in `~/Library/Application Support/DeskPilot/`, readable only by you:
`profiles.json` (your layouts, which include window titles), `settings.json`, and
`log.txt`. Settings, General, **Show Profiles Folder** opens it.

When something goes wrong, send `log.txt` with the report. It records every run, every
Space drag and what the app read on screen, and nothing else. It is capped at a quarter of
a megabyte and never holds a password or a key.

## Updates

Once a day DeskPilot reads its own release list on GitHub. When a newer recommended build
is published it says so once, and Settings, Updates installs it: the download is checked
against this copy's own signature before it replaces the app in Applications and
relaunches. Beta builds carry new features before they are recommended and are offered
only if you tick **Offer beta builds**. Previous versions are listed there too, so you can
go back if a new build does something wrong.

## Known limits

- A Space in **Split View** cannot be moved or separated by DeskPilot. macOS offers no way
  to do it; the app avoids creating one and never drops a Space onto another.
- A fullscreen app is moved by moving its Space. Taking it out of fullscreen and putting it
  back rebuilds the Space at the end of the strip, so DeskPilot does not do that.
- All of an app's windows move to a Space together. A layout that had one app's windows on
  two different Spaces cannot be put back exactly, and the run says so.
