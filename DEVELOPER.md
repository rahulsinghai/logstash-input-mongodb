# logstash-input-mongodb
Example input plugin. This should help bootstrap your effort to write your own input plugin!

## Build new gem

Change version in `logstash-input-mongodb.gemspec`

And build new gem:

```bash
gem build logstash-input-mongodb.gemspec
```

## Developing

### Windows

1. Install JRuby
2. Set environment variables: `JRUBY_HOME` and `PATH=%JRUBY_HOME%\bin;%PATH%`
3. Build the plug-in by running following in Powershell as administrator:

   ```bash
   gem install bundler
   bundle install
   bundle exec rspec
   gem build logstash-input-mongodb.gemspec
   ```

4. Publish the plug-in to Github

   ```bash
   echo ":github: Bearer GH_TOKEN" >> C:\users\rahul\.gem\credentials
   gem push --key github --host https://rubygems.pkg.github.com/rahulsinghai logstash-input-mongodb-0.4.4.gem
   ```

5. Install the plug-in

   ```bash
   .\bin\logstash-plugin install logstash-input-mongodb-0.4.4.gem
   ```

6. Prepare offline pack:

   ```bash
   .\bin\logstash-plugin update
   .\bin\logstash-plugin prepare-offline-pack --output logstash-input-mongodb-0.4.4.zip --overwrite logstash-input-mongodb
   ```

7. Release a new version in Github and upload the .gem & .zip files.

### Use rvm on Ubuntu

1. Install rvm https://rvm.io/

2. Install jruby

```bash
$ rvm install jruby 1.7.25
```

3. Use jruby from rvm

```bash
$ rvm alias create default jruby-1.7.25
$ rvm use default
$ /bin/bash --login
$ gem install bundler
$ bundle install
```

4. Run tests

* Unit
```bash
$ ruby test/*
```

* Rspec (but it needs mongo on localhost, it would be nice to have it is not depended on local mongo)
```bash
$ ./bin/rspec
```

5. Install

```sh
bundle install
gem build logstash-input-mongodb.gemspec
logstash-plugin install logstash-input-mongodb-0.4.4.gem
```