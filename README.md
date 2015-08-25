# gst-project (*Git submodules test - Main project*)

Git submodules are the proper way to link a main project git repository to other git repositories that are libraries/packages/modules shared between different projects.

The basic idea is that the main project repository will be linked to one concrete commit of the submodule. This commit can be changed using typical git commands on the submodule repository like "git checkout" as we will see.

Below you can find the most frequent git commands, and an explanation, to work with git submodules in a typical scenario between different developers. Code snippets are based on a main project called "gst-project" and a submodule project called "gst-submodule".

**Add a submodule to the main project.**

`git submodule add https://github.com/alexmorosmarco/gst-submodule.git`

`git submodule add https://github.com/alexmorosmarco/gst-submodule.git <path to clone the submodule in>`

This command adds a git repository as a submodule of main project and clones it to the current path, inside a folder named as the submodule repository by default. So first code snippet creates a folder called "gst-submodule" on current path and clones the repository inside it. Alternatively we can define other name for the folder as second snippet shows.
Actually it is not same thing as cloning. It clones the code of a concrete commit (last one of master by default), and not the code of the head of a concrete branch. So when pulling the main project the submodule code is also pulled but the linked commit is not updated cause the submodule is frozen at that concrete commit by security.
