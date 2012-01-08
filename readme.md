"tabtabtab", an alternative "tab node creator thingy" for [The
Foundry's Nuke](http://www.thefoundry.co.uk/products/nuke)

It does substring matching (so "blr" matches "blur"), and weights your
most used nodes first (so if I make the useful "Add [math]" node
often, it appears higher in the list than "Add 3:2 pulldown")

# Installation

Put tabtabtab on PYTHONPATH or NUKE_PATH somewhere (maybe in `~/.nuke/`)

Then to your `~/.nuke/menu.py` add:

    import tabtabtab
    m_edit = nuke.menu("Nuke").findItem("Edit")
    m_edit.addCommand("Tabtabtab", tabtabtab.main, "Tab")

This replaces the builtin tab shortcut (you can change the last "Tab"
argument to another shortcut if you wish)

## More elabourate description

With the default "tab thing", you press tab, start typing a node name
(like "Blu") and you get a list of nodes that start with "Blu" (like
"Blur"):

![Nuke's builtin tab thing](imgs/nuke_tab.png)

"tabtabtab" works very similarly, but does substring matching:

![tabtabtab](imgs/tabtabtab.png)

In this example, "tra" finds "Transform" as you'd hope, but also other
nodes, such as "Trilinear"... This is appearing because the letters
"tra" can be found in order, "TRilineAr".

While this seems like it might cause lots of useless results, you
quickly memorise shortcuts like "trear" which matches "TRilinEAR" and
very little else. More usefully, "trage" will uniquely match "TRAnsformGEo"
in an easy to type way, "rdg" matches "ReaDGeo"

The first letter must match, so "geo" will match "GeoSelect", but not
"ReadGeo". However "rgeo" will match "ReadGeo"

## Weighting

Each time you create a node, it's "weight" is increase - the higher
the weight, the higher the node appears in the list.

This means if you create lots of "Add [math]" nodes, it will be
weighted highly, so all you might need to type is tab then "a", and it
will be at the top of the list.

## Matching menu location

If you start typing a shortcut, it will only match the part before the
"[Filter/SubMenu]" (e.g "blf" will not match "Blur [Filter]")

However if you type either "[" or two spaces, you can match against
the menu location (the part in "[...]")

For example, "ax" matches "AddMix [Merge]" and "Axis [3D]". If you
type "ax[3" or "ax 3" (ax-space-space-3) it will only match "Axis
[3D]"
