# code-embers-website

Version control for the KoDa Cast website, which is hosted via Github Pages.

This website utilizes [Hugo](https://gohugo.io/) as its primary framework and either [Castanet](https://github.com/mattstratton/castanet) or [Cloud with Chris](https://github.com/chrisreddington/cloudwithchris.com) as inspiration for its primary architecture and theme. The exact decision will be made based on theme licensing.

## Steps Used to Create This Site

Basically, I'm just following the [Hugo Quick-Start Guide](https://gohugo.io/getting-started/quick-start/) and connecting everything to Git. If on a Mac, make sure you have Homebrew installed, and that your versions of Hugo, Go, and npm are up-to-date.

```terminal
brew install hugo go npm
OR
brew update hugo go npm
```

### Set up Hugo

In a terminal, with Hugo installed, run

```terminal
hugo new site code-embers-website
cd code-embers-website
```

To create a new site and navigate that folder

### Setup Theme vs Module

Add the theme (or update) the module.

Originally, I followed the steps to add a new module, directly connected to the theme. That would be cool...but not complete.

Instead, I'm just copying the theme from the `themes` folder of the [Cloud with Chris Github](https://github.com/chrisreddington/cloudwithchris.com) and building off that.

Their site uses [Git Large File Storage](https://git-lfs.github.com/) to store mp3 its files. I like that concept. To set that up here, I had to first install git-lfs

```terminal
brew install git-lfs
```

and initialize that program via

```terminal
git lfs install
```

Then, in my repo, I set it up to track mp3 files

```terminal
git lfs track "*.mp3"
```

Which created a new `.gitattributes` file. If you don't see that, you should also run

```terminal
git add .gitattributes
```

...though that last step was unnecessary for me

### Setup Hugo Modules / Pipes

First, check to make sure that your version of Hugo has the 'extended' tag on it when you run `hugo version`. If not, you may need to install this manually instead of via a package manager (such as Homebrew).

You need to initialize Go within the root directory of your repo. The `code-embers-website` portion can be named whatever you want.

```terminal
hugo mod init code-embers-website
```

Running `hugo serve` still gave me errors at this point, providing the message

```terminal
Error: Error building site: TOCSS: failed to transform "sass/main.scss" (text/x-scss): SCSS processing failed: file "stdin", line 4, col 1: File to import not found or unreadable: bootstrap/bootstrap.scss.
```

and later

```terminal
Error: Error building site: TOCSS: failed to transform "sass/main.scss" (text/x-scss): SCSS processing failed: file "stdin", line 7, col 1: File to import not found or unreadable: fontawesome/fontawesome.scss.
```

This is because I needed to install bootstrap and fontawesome manually via npm. I did this via

```terminal
npm install bootstrap @fortawesome/fontawesome-free
```

Finally, I am now able to run

```terminal
hugo serve -D
```

without issue. Note that the `podcast_site_template` branch of this repo shows exactly where I 'landed' after running the above steps and clearing out the unique content from the `config.yaml` page.

### Next Steps

I'll need to update the site with the relevant links, pages, and assets to make this unique to my own efforts, as well as the various themes/color schemes that fit with a water/lake motif instead of clouds.

For now, I'm going to keep the `themes/cloud-with-chris` folder a locally sourced asset, since there are many elements that are unique to the Cloud with Chris website and would not work well on a custom site. I'll keep these modifications so any can review...though for now I'm going to start with it in `.gitignore` so as to space my commit history a bit. If I didn't need to make so many custom modifications, I probably would have just used this theme as its own Hugo module...made available in the `config.yaml` folder and pointing to the Github repo with that theme. There are other assets in that YAML file with `source:` and `target:` locations that you can use for inspiration here.

If you want to build from that branch to make your own podcasting website, please feel free. These efforts build on the excellent works of [Chris Reddington](https://github.com/chrisreddington) for his [Cloud with Chris podcast](https://github.com/chrisreddington/cloudwithchris.com), which itself builds on [Matt Stratton's](https://github.com/mattstratton/) work on the [Castanet podcast](https://github.com/mattstratton/castanet). All of these are under the MIT license. Build away!

More content to come...
