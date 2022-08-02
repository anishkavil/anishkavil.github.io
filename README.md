
## Setting up your local workstation to use Jekyll.

1. Install Ruby other than what is there on you local machine.
2. Install your own ruby with brew install ruby and change the path in your bash file.
```shell
if [ -d "/usr/local/opt/ruby/bin" ]; then
  export PATH=/usr/local/opt/ruby/bin:$PATH
  export PATH=`gem environment gemdir`/bin:$PATH
fi
```
<sub>Installing Ruby on Mac : https://mac.install.guide/ruby/13.html</sub>

3. Install bundler and jekyll
```shell
$ gem install bundler jekyll
```
4. Install all other dependencies
```shell
bundle install
```
5. bundle add webrick . if you get this error
```shell
$ bundle exec jekyll serve --trace
Configuration file: none
           Source: /Volumes/TranscendSD/projects/jktest
      Destination: /Volumes/TranscendSD/projects/jktest/_site
Incremental build: disabled. Enable with --incremental
     Generating...
                   done in 0.059 seconds.
Auto-regeneration: enabled for '/Volumes/TranscendSD/projects/jktest'
bundler: failed to load command: jekyll (/usr/local/lib/ruby/gems/3.1.0/bin/jekyll)
/usr/local/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/commands/serve/servlet.rb:3:in `require': cannot load such file -- webrick (LoadError)
 from /usr/local/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/commands/serve/servlet.rb:3:in `<top (required)>'
 from /usr/local/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/commands/serve.rb:179:in `require_relative'
 from /usr/local/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/commands/serve.rb:179:in `setup'
 from /usr/local/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/commands/serve.rb:100:in `process'
 from /usr/local/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/command.rb:91:in `block in process_with_graceful_fail'
 from /usr/local/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/command.rb:91:in `each'
 from /usr/local/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/command.rb:91:in `process_with_graceful_fail'
 from /usr/local/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/commands/serve.rb:86:in `block (2 levels) in init_with_program'
 from /usr/local/lib/ruby/gems/3.1.0/gems/mercenary-0.4.0/lib/mercenary/command.rb:221:in `block in execute'
 from /usr/local/lib/ruby/gems/3.1.0/gems/mercenary-0.4.0/lib/mercenary/command.rb:221:in `each'
 from /usr/local/lib/ruby/gems/3.1.0/gems/mercenary-0.4.0/lib/mercenary/command.rb:221:in `execute'
 from /usr/local/lib/ruby/gems/3.1.0/gems/mercenary-0.4.0/lib/mercenary/program.rb:44:in `go'
 from /usr/local/lib/ruby/gems/3.1.0/gems/mercenary-0.4.0/lib/mercenary.rb:21:in `program'
 from /usr/local/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/exe/jekyll:15:in `<top (required)>'
 from /usr/local/lib/ruby/gems/3.1.0/bin/jekyll:25:in `load'
 from /usr/local/lib/ruby/gems/3.1.0/bin/jekyll:25:in `<top (required)>'
 from /usr/local/lib/ruby/gems/3.1.0/gems/bundler-2.3.19/lib/bundler/cli/exec.rb:58:in `load'
 from /usr/local/lib/ruby/gems/3.1.0/gems/bundler-2.3.19/lib/bundler/cli/exec.rb:58:in `kernel_load'
 from /usr/local/lib/ruby/gems/3.1.0/gems/bundler-2.3.19/lib/bundler/cli/exec.rb:23:in `run'
 from /usr/local/lib/ruby/gems/3.1.0/gems/bundler-2.3.19/lib/bundler/cli.rb:483:in `exec'
 from /usr/local/lib/ruby/gems/3.1.0/gems/bundler-2.3.19/lib/bundler/vendor/thor/lib/thor/command.rb:27:in `run'
 from /usr/local/lib/ruby/gems/3.1.0/gems/bundler-2.3.19/lib/bundler/vendor/thor/lib/thor/invocation.rb:127:in `invoke_command'
 from /usr/local/lib/ruby/gems/3.1.0/gems/bundler-2.3.19/lib/bundler/vendor/thor/lib/thor.rb:392:in `dispatch'
 from /usr/local/lib/ruby/gems/3.1.0/gems/bundler-2.3.19/lib/bundler/cli.rb:31:in `dispatch'
 from /usr/local/lib/ruby/gems/3.1.0/gems/bundler-2.3.19/lib/bundler/vendor/thor/lib/thor/base.rb:485:in `start'
 from /usr/local/lib/ruby/gems/3.1.0/gems/bundler-2.3.19/lib/bundler/cli.rb:25:in `start'
 from /usr/local/lib/ruby/gems/3.1.0/gems/bundler-2.3.19/exe/bundle:48:in `block in <top (required)>'
 from /usr/local/lib/ruby/gems/3.1.0/gems/bundler-2.3.19/lib/bundler/friendly_errors.rb:120:in `with_friendly_errors'
 from /usr/local/lib/ruby/gems/3.1.0/gems/bundler-2.3.19/exe/bundle:36:in `<top (required)>'
 from /usr/local/lib/ruby/gems/3.1.0/bin/bundle:25:in `load'
 from /usr/local/lib/ruby/gems/3.1.0/bin/bundle:25:in `<main>'
```
## Creating a Basic Site

  1. Create a Directory to host all the files created
  2. Switch to that directory
  3. Create a new Gem file
	   ``` shell
	   $ bundle init
	   ```
  4. The above step would create a Gemfile in your directory
  5. Edit the Gemfile and add jekyll as dependency to do that add in the Gemfile.
    ```shell
    $ gem jekyll
    ```
  6. Add a sample HTML file in your directory
  7. To build Jekyll site
    ```shell
     $ jekyll build
     ```
  8. To start the server for your site
    ```shell
    $ bundle exec jekyll serve
    ```
  9. If everything allright your should get this
    ```shell
    $ bundle exec jekyll serve
    Configuration file: /Volumes/TranscendSD/projects/anishkavil.github.io/_config.yml
    To use retry middleware with Faraday v2.0+, install `faraday-retry` gem
           Source: .
      Destination: ./_site
      Incremental build: disabled. Enable with --incremental
      Generating...
                   done in 7.939 seconds.
      Auto-regeneration: enabled for '.'
      Server address: http://127.0.0.1:4000/
      Server running... press ctrl-c to stop.

    ```
