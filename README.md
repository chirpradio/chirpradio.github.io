# chirpradio.github.io
Developer documentation and wiki in Jekyll hosted on Github Pages

View the site here: https://chirpradio.github.io/

## Handy Documentation Links
[Documentation for Github Pages](https://docs.github.com/en/pages)
[Documentation for Jekyll](https://jekyllrb.com/docs/), the Ruby-based static site generating language that the wiki is built on. NOTE: Not all Jekyll functionality works on Github Pages.
[Documentation for Just The Docs](https://just-the-docs.com/), the specific gem template the wiki is using
[Markdown Cheat Sheet] (https://www.markdownguide.org/cheat-sheet/)

## How to Contribute

### Edit files in the Github GUI
This is best for minor changes or adding/editing content on existing pages.

1. Navigate to the page you want to edit
2. Click "Edit this page on Github"
3. You will be routed to the file in Github. Click the "Edit this page" pencil icon in the top-right corner.
4. Modify the file to your liking. All the pages support standard markdown, but special functionality for Jekyll and our template can be found in the docs above.
5. When finished, click the green "Commit Changes" button.
	- Add a commit message. Try to be brief but informative, please!
	- Choose where to commit your changes. If you select "Commit directly to the main branch", your changes will be published immediately. If you commit to a new branch, you will need to open a pull request for the changes and merge it into main for your changes to be published.
6. Navigate to the page you updated to check over your changes and ensure everything is working correctly. Please note, changes may take up to ten minutes to appear on the site.

### Run the site locally and push changes
This is best for major changes, adding new pages, or adding functionality.

##### Requirements:
- Ruby v3.2.3 (recommend using [rbenv](https://github.com/rbenv/rbenv) to manage Ruby versions, if you don't have a preferred version manager on your machine)

1. Clone this repo
2. Make desired changes directly to the code
3. To preview your changes locally, navigate to your local repo and run `bundle exec jekyll build && bundle exec jekyll serve` to build the site and start the server. You may need to install bundler or bundle install the gems from the Gemfile the first time you do this (`gem install bundler` then `bundle install`)
4. Visit `localhost:4000` You should be able to see your local changes here. The preview should update on file save, so new changes should get pulled in as you refresh. There may be some delay. Where your server is running, you will be able to see it rebuilding the files as they're saved. All the pages support standard markdown, but special functionality for Jekyll and our template can be found in the docs above.
5. When finished, commit and push changes to Github. Changes pushed to the main branch will publish to the site automatically. If you commit to a new branch, you will need to open a pull request for the changes and merge it into main for your changes to be published.
6. Navigate to the page you updated to check over your changes and ensure everything is working correctly. Please note, changes may take up to ten minutes to appear on the site.

## Troubleshooting

*Q: I pushed some changes to main, but they're not showing up on the site. What gives?!*
*A:* First off, changes can take up to ten minutes to show up on the site. If it's been more than ten minutes, try checking the workflow runs [here](https://github.com/chirpradio/chirpradio.github.io/actions) (can also be found under "Actions" tab at the top of the repo.) The workflow action for "pages build and deployment" will automatically run whenever changes are pushed to the main branch. Check that a workflow action is listed for your change, and that it has a green check mark. If it's showing a red X, that means something failed during build and deployment. You can click on it to view associated error messages, and find out what went wrong.

*Q: When I try to build and start the Jekyll server locally, I get an error like "Could not find 'bundler' (2.5.5) required by your chirpradio.github.io/Gemfile.lock. (Gem::GemNotFoundException)"*
*A:* You will need to install bundler and/or bundle install gems before trying to run Jekyll. Try `gem install bundler` then `bundle install` (the error may give you more specific instructions, like what specific version of bundler to install, in which case follow those instructions.)

*Q: When I try to install bundler or run `bundle install`, I get an error like "ERROR:  While executing gem ... (Gem::FilePermissionError)
    You don't have write permissions for the /Library/Ruby/Gems/2.6.0 directory."*
*A:* Your computer is trying to use its system Ruby to install the gems, which is usually not a good idea and generally prohibited. Consider installing a Ruby version manager, like rbenv, if you don't already have one. If you do have one, make sure it is currently set to use a different Ruby than the system Ruby on your computer. There is a .ruby-version file in this repo that should automatically specify what version to use, so your version manager may prompt you to install a specific version when you navigate into the repo.