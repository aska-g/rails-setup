## Checklist before you start

 - Global gitignore in your home directory `~/.gitignore_global` .ie this:  https://github.com/rubynor/rails-setup/blob/master/.gitignore_global


### Our prefered rails setup

1. Generate the app with vue and webpacker

```
rails new the-rubynor-app --webpack=vue --skip-test --database=postgresql
```

2. Initial commit and prep work

```
cd the-rubynor-app
cp config/database.yml config/database.yml.sample
git init .
git diff # double check that database.yml is ignored. Did you put the .gitignore_global in your home dir?
git commit -am "ran rails new"
```    


2. Copy the gemfile and bundle install. Here is our recomendation: 
 https://github.com/rubynor/rails-setup/blob/master/Gemfile

``` 
#Append the recommend Gemfile gems to your gemfile
curl -sS https://raw.githubusercontent.com/rubynor/rails-setup/master/Gemfile >> Gemfile
#check if this makes sense, you might want to move things around, especially to ensure only one group :development, :test 
git diff 
bundle install
git commit -am "install recommended gems"
```    

3. Run the following commands

```
rails generate haml:application_layout convert
rm app/views/layouts/application.html.erb # as the above script instructs you to do manually
rails generate rspec:install
bundle exec guard init rspec
git add.
curl -sS https://raw.githubusercontent.com/rubynor/rails-setup/master/.rspec > .rspec
git diff
git commit -am "install haml and rspec"
```

### Honeybadger
Go to https://app.honeybadger.io/projects/new

bundle exec honeybadger install [secret]

### Environment variables
We use `dotenv-rails` to manage environment variables.

Create a file named `.env` and put them there. Remember to add a .env.sample that is added to the repo

### Foreman
Foreman will let you start both rails server and the webpack server in one command.

Foreman should not be added to you Gemfile, it should be installed as a global gem on your pc.

```
gem install foreman
```

Copy `Procfile` and `.foreman` to your repo and run:

```
foreman start
```

### Capybara
In your test helper file you have to add the following
```
require 'capybara/rails'
```
