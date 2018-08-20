# scala-training

Howdy!

Welcome to Comcast! \o/

This is a small collection of Scala training materials put together by kf, mostly intended to onboard new interns for Summer 2013.

## Downloading the Materials

You have two options for downloading the materials: Git or as a ZIP file. If you're new to Comcast, you'll probably want to learn how to use Git!

#### Installing Git

Git is a free and open-source distributed version control system, which allows everyone on our team to collaborate on the same code base simultaneously. It's also super-great to use on personal projects, because if you accidentally delete or mangle your code, you can just revert to a previous version! \o/

If you haven't already, you can download Git by downloading the installer from the [official website](https://git-scm.com/). Follow the prompts, and you should be good to go!

#### Actually Downloading the Materials

First, "fork" the repository into your own account by heading to https://github.comcast.com/kfello201/scala-tutorial and clicking on "Fork" in the upper-right corner. Once the repository has been forked, you can download it by copying the HTTPS clone URL from the bottom-right corner, then navigating to your local projects directory

```
$ cd src
```

and running

```
$ git clone https://github.comcast.com/your-ntid/scala-tutorial.git
```

If you `cd` into the new directory `scala-tutorial`, you'll be able to poke around the materials!

## Navigating the Materials

The materials are organized into several directories, each named `stage-*`.

Aside from `stage-1`, which is the installfest, the directories are independent units--meaning, `stage-4` does not depend on your code or configuration in `stage-2` or `stage-3`, and vice-versa.

Accordingly, you should be able to `cd` into each stage and start fresh as new material is discussed.