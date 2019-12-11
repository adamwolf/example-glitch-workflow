# example-glitch-workflow

I really like Glitch. I love how easy it is to put some code on the internet and have it run!

However, I am looking for something a little more deliberate than the typical Glitch workflow.

The idea here is that I have one repository where all my code lives.  I also have two Glitch projects.
One reflects development, and can have changes all willy-nilly.  When I'm ready to "save", I export to
Github from Glitch, which makes a commit to the 'glitch' branch over at Github.  I can then make a Pull
Request (PR) from the glitch branch over to the master branch, where folks can review it and give feedback,
and then when that's merged into master, a little automation pushes the changes to master to a second 
Glitch project.

This means that I can do work on Glitch, get interrupted, and not have to worry that I broke my Glitch project.
My changes will be on the development project, not the master project.

(This also is a workflow that may help some junior devs transition to a more enterprisey type environment.)

## How to set this up
I'm assuming you're starting with an example project on Glitch.

Make a project, called foo-dev.  The first project is the development project.  This is one where folks can edit 
live on Glitch and see
their changes super fast.  You'll have to set up the link to Github.  If you haven't created a repository
at Github, go do that.  If you don't have any files to put in it yet, make sure to click the "initialize project
with README" during Github repository creation.  Once you have a Github repository, with a file in it, go to 
Tools > Git, Import, and Export > Export to Github
and set up the link to Github.

Export foo-dev to Github.  Go to Github, make a PR from glitch into master, and accept it.  Tada! Thats how you'll
be making all of your changes... but after we set it up, the next part will be automatic.

Make another project, called foo.  This is your master project.  Go to Tools > Git, Import, and Export > Import from Github
and import from your project.

SETUP GITHUB ACTION

## How to use this once it's set up

Make your changes in Glitch, on foo-dev.  When you're ready with them, go to Tools > Git, Import, and Export > Export to Github.
Every time you export to Github from glitch, it writes to the 'glitch' branch over at Github.  It asks you for a
commit message even, so you can explain what you've done!

Wait a moment, and the Github Action will run, and take what's on master on Github and put it on Glitch, on foo!

Don't edit source on foo, after you've got it set up. Any changes you make will just be overwritten after the next commit.  
Consider limiting who can edit the master project.

# How do I get changes from other people?

Once this gets fleshed out, this is going to be awesome.

If someone forks your repository and sets it up on Glitch, they can issue a PR to your repository.  
You accept it, and the changes will show up on master!

There's a snag here, where we have to pull those changes into the development project, and also
someone better versed in Glitch than myself probably knows how to make this easy to set up for
folks who don't use git everyday.

If you are that person, I'd love to hear your thoughts, or better yet, see a PR from you! :)

# Resources

This project uses the wonderful https://github.com/glitch-tools/sync-glitch-github-action.