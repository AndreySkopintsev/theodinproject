# [The Odin Project](http://theodinproject.com)
*[http://theodinproject.com/](http://theodinproject.com)* [version 0.0.7]

### The Open Curriculum for Learning Web Development


This site provides the main user experience for The Odin Project, including the home page and all user functions.  It is meant to be a shell around [The Odin Project Curriculum](https://theodinproject.com/curriculum) and to include the tools that help students to pair together and get to know others who are working on the curriculum.  

It has been open-sourced to provide both a learning resource for students who want to see how the tools they're using are built and to give students the opportunity to stretch their wings and contribute to a real open-sourced project... while building the tools they themselves will be using.

Thus far, the code has been more or less hacked together so don't use it as a star example of how things should be done!  We'll be rolling out some better documentation and contribution instructions as this develops a little further.

For minor fixes, either submit a github issue or a pull request.  Please coordinate with the project maintainers if you're interested in working on some of the larger features in order to avoid traffic jams.

Contact us directly at [project@theodinproject.com](mailto:project@theodinproject.com)

## Future Development

The file [dev_roadmap.md](dev_roadmap.md) will be more specific but there are some overall goals for the short term development of this project:

* Start rolling out realtime collaboration features and progress tracking for students who are using the curriculum.
* Improve test coverage, particularly for the curriculum and the scheduling tool (which is all javascript).
* Improve the documentation of the existing code base so people can more easily navigate through it.  This means in-line commenting and also creating a higher level github wiki page that explains how the project works and the best ways to navigate it.

If you'd like to help out (even as a relative newbie), please [get in touch](mailto:contact@theodinproject.com) and we'd be happy to point you in the right direction.

### Hacking on the Site Yourself

1. This site runs on Ruby 1.9.3 and Rails 3.2.12.
1. Download the repo to your local machine by doing a `git clone git@github.com:TheOdinProject/theodinproject.git`
2. Run a `$ bundle install` of all the gems
1. Note: Both local and production databases are [Postgres](http://www.postgresql.org/docs/), so if you're used to just using Rails' default SQLite database you'll need to get Postgres fired up on your local machine.  The major difference is that Postgres operates almost like a server, so you'll need to download a client for it and create a `theodinproject` database that the application can connect to.  Ryan Bates has a [RailsCast](http://railscasts.com/episodes/342-migrating-to-postgresql) episode about migrating to Postgres that may be helpful if you're a newbie.  If you're deployed on Heroku (which we are), you need to use PG anyway.
2. Once you've got postgres installed and have created the empty database, run a `$ rake db:migrate` to run all the migrations that will set up the schema properly.  I haven't yet created any seed data you can prepopulate the database with (like users).  Make a pull request if you've put together a useful `db/seeds.rb` file!
3. The Moot forums and Github API calls rely on private environment variables that you won't find in the repo. I upload them directly to the server myself using the `figaro` gem and a corresponding file called `application.yml` that's located in the `config/` directory but not checked into git (no, you can't have my passwords).  Check out the [Figaro Documentation](https://github.com/laserlemon/figaro) for a very easy-to-understand explanation of how the gem works.  You basically just need to run `$ rails generate figaro:install` and populate the missing variables to `application.yml`.  An example, as of this writing:

        # config/application.yml
        moot_api_key: UjI8SKQv6J
        moot_secret_key: no_you_cant_have_my_secret_key
        GITHUB_API_TOKEN: your_token_would_go_here

You can create your own "personal access token" [HERE](https://github.com/settings/applications).  It's being used here to increase the number of calls we can make to the Github API to access the curriculum each hour.  As for the moot key... you may not be able to use the forums feature without one.  Anyone have ideas how to get around that?

1. Run a `$ rails server` and see if that lets you check out the app at `http://localhost:3000`.
1. That... should... be... it...?

*I haven't had to clone and start from scratch yet so please let me know what I've missed here!*

## Features

The scheduling tool allows users to sign up and show when they're available to pair up on projects.  

### Referral Link
You can set up a referral link so that someone can click on it and get taken directly to the scheduler with that project already added to their list.  To do so, just use the format:

`http://www.theodinproject.com/?cb=[id of project]`

...where `[id of project]` should be the ID of the project (called a "content_bucket" in the schema) you'd like them to work on directly.  If I wanted to have someone work with me on the edX SAAS homework assignment #4, I would use the link:

`http://www.theodinproject.com/?cb=6`

Using IDs is obviously not ideal but it's the best we've got right now.  If you're wondering which project goes with which ID, your best bet right now is to guess-and-check by following those links... there aren't too many projects so it shouldn't be too tough.

<hr>
Created by [Erik Trautman](http://www.github.com/eriktrautman)