# example-glitch-workflow

#### Adam Wolf, 2019

I am not a Glitch expert, and I'd love tips or help improving the following.

I really like Glitch. I love how easy it is to put some code on the internet and have it run!

However, I am looking for something a little more deliberate than the typical Glitch workflow.

The idea here is that I have one repository where all my code lives. I also have two Glitch projects. One reflects development, and can have changes all willy-nilly. When I'm ready to "save", I export to Github from Glitch, which makes a commit to the 'glitch' branch over at Github. I can then make a Pull Request (PR) from the glitch branch over to the master branch, where folks can review it and give feedback, and then when that's merged into master, a little automation pushes the changes to master to a second Glitch project.

This means that I can do work on Glitch, get interrupted, and not have to worry that I broke my Glitch project. My changes will be on the development project, not the master project.

(This also is a workflow that may help some junior devs transition to a more enterprisey type environment.)

## How to set this up

I'm assuming you're starting with an example project on Glitch.

Make a project, called foo-dev. The first project is the development project. This is one where folks can edit live on Glitch and see their changes super fast. You'll have to set up the link to Github. If you haven't created a repository at Github, go do that. If you don't have any files to put in it yet, make sure to click the "initialize project with README" during Github repository creation. Once you have a Github repository, with a file in it, go to Tools > Git, Import, and Export > Export to Github and set up the link to Github.

Export foo-dev to Github. Go to Github, make a PR from glitch into master, and accept it. Tada! That's how you'll be making all of your changes... but after we set it up, the next part will be automatic.

Make another project, called foo. This is your master project. Go to Tools > Git, Import, and Export > Import from Github and import from your project.

### Setting up Github Actions

This is where the magic happens! (However, it requires some nitty-gritty to set up.)

You are going to set up a Github Action workflow. You will need a file that I've made, plus you'll need two pieces of information from your master Glitch project. These are sensitive, kinda like passwords, so don't give them to people.

You will need your "Glitch Token" and your "Glitch Project ID". The way I know how to get them is as follows:

1. Go to your master project on Glitch.
2. Open up your web browser's console. If on Chrome, try right clicking on the page and selecting Inspect.
3. Import from Github in Glitch.
4. (This is the complicated one. Sorry, folks!) In the Network tab of the console in your web browser, look for the request starting githubImport?projectId... There should be two of them. One of them is a POST, and the other is OPTIONS. You can tell the difference by clicking on them, and then in the side pane, under General, it tells the Request Method. Click on the POST. Scroll down to the very bottom, under Query String Parameters, there is a projectID. That's your Glitch Project ID. Scroll up a bit, and under Request Headers, there's an authorization. That's your Glitch Token. Remember, these are like passwords, so don't give them out.
5. Go into your Github project, and go into Settings. Under Secrets, Add A New Secret, and make one called GLITCH_PROJECT_ID. Paste in your project ID as the value. Make another new secret called GLITCH_TOKEN, and paste in your Glitch token.

Phew!

Now, go to your Github repo, and we're going to copy in the workflow file. You can use the web interface to create a new file. Have it go into .github/workflows/workflow.yml, and copy the contents of <https://raw.githubusercontent.com/adamwolf/example-glitch-workflow/master/.github/workflows/workflow.yml> into it. If you want, change the URL in the name to point at your master Glitch so you can remember how this all goes together when you look at it in six months. :)

## How to use this once it's set up

Make your changes in Glitch, on foo-dev. When you're ready with them, go to Tools > Git, Import, and Export > Export to Github. Every time you export to Github from glitch, it writes to the 'glitch' branch over at Github. It asks you for a commit message even, so you can explain what you've done!

Wait a moment, and the Github Action will run, and take what's on master on Github and put it on Glitch, on foo! You can look at it working on the Actions tab of your Github Repo.

# Is there anything I should watch out for?

Don't edit source on foo, your master Glitch, after you've got it set up. Any changes you make will just be overwritten after the next commit. Consider limiting who can edit the master project.

If you edit source on Github or through other PRs that don't originate from the develop Glitch, you'll probably want to pull those in. You can do that using Import from Github on the develop Glitch site.

It seems to be working fine with .env files. You'll need to edit those using Glitch, and they aren't imported or exported (like you'd expect.) Before putting anything sensitive in there, do a test for yourself.

# How do I get changes from other people?

Once this gets fleshed out, this is going to be awesome.

If someone forks your repository and sets it up on Glitch, they can issue a PR to your repository. You accept it, and the changes will show up on master!

There's some snags here. We have to pull those changes into the development project. Someone better versed in Glitch than myself probably knows how to make this easy to set up for folks who don't use git everyday. If you are that person, I'd love to hear your thoughts, or better yet, see a PR from you! :)

# How do I ask questions about this?

Hmm. I'm not sure. Maybe go file an issue over at <https://github.com/adamwolf/example-glitch-workflow/issues>?

# Resources

This project uses the wonderful [Sync Glitch Github Action](https://github.com/glitch-tools/sync-glitch-github-action) and [markdown-webpage](https://glitch.com/edit/#!/markdown-webpage).
