Git submodules are the proper way to use git repositories that are libraries/packages/modules from a main project git repository.

The basic idea is that the main project repository will be connected to one concrete commit of the submodule. This commit can be changed using typical git commands on the submodule repository like "git checkout" as we will see.

Below you can find the most frequent git commands and an explanation, to work with git submodules in a typical scenario between several developers. Code snippets are based on a main project called *"gst-project"* and a submodule project called *"gst-submodule"*.

##Add a submodule to the main project.

**`git submodule add https://github.com/alexmorosmarco/gst-submodule.git`**

This command adds a git repository as a submodule of main project and clones it to the current path, inside a folder named as the submodule repository name by default. So in the above example it creates a folder called *"gst-submodule"* on current path and clones the repository inside it.

Actually it is not same thing as cloning. It clones the code of a concrete commit (last one of master branch by default), and not the code of the head of a concrete branch. So when pulling the main project the submodule code is also pulled but the connected commit is not updated cause the submodule is frozen at that concrete commit by security.

**`git submodule add https://github.com/alexmorosmarco/gst-submodule.git <path_to_submodule>`**

Alternatively we can define other name for the folder as an additional parameter.

##Check the status of the submodules

**`cat .gitmodules`**

The command *"git submodule add"* creates a new file called *".gitmodules"* which contains the information of the submodules (local and remote paths and names). Yo can have a look at it to see that information.

**`git submodule status`**

Prints the pointed commit SHA of every submodule of the main project.

##The typical scenario between several developers.

1. **1st developer adds submodules to the main project**
2. **2nd developer prepares his local copy**
  1. Clone the main project
  2. `git submodule init`

     Initialize the submodules based on the content of the file ".gitmodules". This command does not clone/download any code.
  3. `git submodule update`

     Clone the submodules repositories if their code is not in local, so if their code has not been checked out. If the code had already been checked out then it just points the submodule local repository to the commit that is defined for this submodule in the main project. If their code has had new commits and I have not checked them out, I need to do a git pull of the main project before doing a git submodule update.
3. **1st developer modifies a submodule and pushes it**
  1. Commit and push the changes on the submodule git repository
  2. Commit and push the submodule folder on main project git repository, which contains the pointed commit SHA of the submodule.
4. **2nd developer updates to last changes on the submodules**
  1. `git pull`

      On main project folder. It will pull the main project code and also the submodules code. Intead of this you can do "git fetch" and then merge the branches as you need, but take into account that the submodules folders of main project need to be checked out so that git can update later the submodules.
  2. `git submodule update`

     It updates the submodules to the pointed SHA commit by the main project.


