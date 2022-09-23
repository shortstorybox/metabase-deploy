# SHORT STORY INSTRUCTIONS

 - To rebase our patches with new Metabase code, run the following in the
   `metabase` repository. (That's a different GitHub repository from this one):

     $ git fetch upstream
     $ git rebase --onto upstream/master master shortstory-patches
     $ git switch master && git merge --ff-only upstream/master && git switch shortstory-patches
     $ git push origin master shortstory-patches

 - To run metabase locally, run the following. But be careful! This uses the
   production database that stores all our Metabase settings:

     $ cd ../metabase-deploy && ln -s ../metabase/target ./target
     $ cd ../metabase && bin/build && cd ../metabase-deploy && env -S "$(heroku config --shell --app shortstory-metabase-dev)" bin/start

 - To make a new release, run the following in the `metabase` repository:

     $ bin/build
     $ git tag v1.44.3-shortstory-patch-2   # (or whatever the current patch name should be)
     $ git push origin --tags

   Then create a new release at
   https://github.com/shortstorybox/metabase/releases and attach the newly
   compiled file target/uberjar/metabase.jar to the GitHub release.

   Then open `bin/compile` in the `metabase-deploy` repository, and update
   `METABASE_VERSION=` to match the tag you created above. Push this change to
   the metabase-deploy GitHub repository.




[![Metabase Logo](http://www.metabase.com/images/logo.svg)](http://www.metabase.com/)

[Metabase](http://www.metabase.com/) is the easy, open source way for everyone in your company to ask questions and learn from data.

# Running Metabase on Heroku

[Heroku](https://www.heroku.com/home) is a great place to evaluate Metabase and take it for a quick spin with just a click of a button and a couple minutes of waiting time. If you decide to keep your Metabase running long term we recommend some upgrades as noted in the documentation linked to below to avoid limitations of the Heroku free tier.

*tl;dr Click this button to deploy Metabase to Heroku for free.*

[![Deploy to Heroku](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

For more details, check out the [Heroku-specific deploy documentation](http://www.metabase.com/docs/latest/operations-guide/running-metabase-on-heroku.html) for help with:
* Upgrading beyond Heroku's free plan
* Deploying Metabase version updates to Heroku
* Troubleshooting
