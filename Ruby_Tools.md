**RubyGems** 

- a library of code packages called gems which can be downloaded within Ruby programs using the keyword `require` or from the command line. The `gem` command from the command line interface (CLI) manages, installs, and manipulates code packages. 

- RubyGems is a model for how to package our own gems.  All Ruby projects use RubyGems as a standardized template, format, and structure. 
- Code packages that can be downloaded and installed. 
- Managed with the `gem` command. Install a new one with `gem install <gem-name>` (available gems found on RubyGems website)

**Your Gems**

When a new gem is installed, it puts all the files that make up that Gem into a local gem library.

This location is determined by what version of Ruby you are using and if you're using a RVM- This local gem library allows you to look at gem source code or diagnose a problem with the gem. Type `gem env` to find out: 

- `RUBY VERSION` = shows the version number of the Ruby associated with the `gem` command (recall that each Ruby has it's own version of `gem`)
- `RUBY EXECUTABLE` = location of the `ruby` command you should use with this particular `gem` command.
- `INSTALLATION DIRECTORY` = where `gem` installs Gems
- `USER INSTALLATION DIRECTORY` = if `gem` installs gems in your home directory instead of on a system level
- `EXECUTABLE INSTALLATION DIRECTORY` = Where `gem` stores commands that can be used directly from the CLI. Should be included in the shell `PATH` variable (this is usually handled by RVM)
- `REMOTE SOURCES` = Remove lib used by the `gem` installation
- `SHELL PATH` = value of the shell `PATH` variable

Gems, like Ruby, also have specific versions. Different  programs may rely on different versions and running the wrong version of a Gem with a given program may cause issues.

The full path name of the gem your program loaded can provide information about the specific Gem version. Use `puts $LOADED_FEATURES.grep(/<name_of_gem>\.rb/)` somewhere in the program after `require` to output the full pathname for the Gem in question.

Bundler is a gem that helps us manage programs that rely on features from different versions of Gems.

**Ruby Version Managers**

- pieces of software that help us deal with multiple versions of Ruby installed on our local system.  We want to make sure that our project is the same version that we are running on our system. 
- Bundler installs all the necessary components and makes sure we are using the correct version of Ruby 

**Rake**

- A gem that allows us to automate repetitive tasks having to do with building, testing, packaging, and installing a project. These tasks are defined in a `Rakefile` which uses a DSL (Domain Specific Language) to define 'taks' (these tasks are just ruby programs) that can be executed from the command line with `rake`

**.gemspec**

`.gemspec` is a file that is included in Gem projects. It provides info such as name, summary, authors, contact info about a Gem. If you want to release a program or library as a Gem, you must incliude a `.gemspec` file. 

**Installation**

- Use a Ruby Version Manager(RVM or RBENV) to install Ruby.  Use this over a system version of Ruby, which can be outdated or require root access.

- If you type `which ruby` into CLI and get `/usr/bin/ruby`, then you are using a system version of ruby 

- run `ruby -v` to see what version you are running 

- Every Ruby installation comes with: 

  - `ruby` command = runs Ruby programs
  - The core library = built-in objects, classes, and methods)
  - The standard library = object, classes, and methods you can `require`)
  - The `irb` REPL = test small snippets of code
  - `rake` utility = runs automated tasks you have specified in the `Rakefile` of a project
  - `gem` command =  a tool to manage RubyGems
  - `rdoc` and `ri` = documentation tools

  

**Reasons for Ruby Version Managers**

These are programs that help us install, manage, and organize multiple versions of Ruby on the same local system (utilities included with a particular version and any Gems installed)

- Ruby is an ever-changing language and some non-universal features may necesitate differenet versions
- Programs being worked on by multiple developers need standardization
- Working on multiple projects that use different versions of Ruby may necesitate different versions. 

Version managers allow us to quickly and easily install and uninstall Ruby versions, and run whichever Ruby we need within a specific environment.

The two main RVM's are :

1) RVM - includes more features and works by dynamically managing your development environment
2) RBENV- does not include as many features, but allows you to install `plugins` that give more functionality. Works by modifying your environment variables (`$PATH`)

**Bundler**

A gem that works as a "dependancy manager". It helps simplify the installation and environment usage of different multiple versions of Ruby and Gems for any given project.

- specifies which Ruby and which Gems you want to use with a Ruby program
- installation of multiple versions of each gem under a specific version of Ruby 
- You must install Bundler by running `gem install bundler` on the CLI for each version of ruby that you use. 

**Gemfile and Gemfile.lock**

To use Bundler, we have to include a `Gemfile` in our project directory. This utilizes a specific Bundler DSL to list the Ruby and Gem versions that a particular project uses. It functions as a configuration file for Bundler. 

- `source` = the remote library where any gems to be installed can be found (most usually, `https://rubygems.org`).
- `ruby` = tells what Ruby version you want the program to use
- `gem` = tells the gem name and the version you want the project to use
- Note that each individual gem the project utilizes needs it's own `gem` statement.
- `gemspec` = statement that tells the `Gemfile` if there is a `gemspec` file

```ruby
source 'https://rubygems.org'

ruby '2.3.1'
gem 'sinatra'
gem 'erubis'
gem 'rack'
gem 'rake', '~>10.4.0'
```

Once we have the `Gemfile`, we run `bundle install` on the command line to create a `Gemfile.lock`. This will include information on *all* the dependencies within a project, including any other Gems that the Gems listed in the `Gemfile` will need to function.

If there are any changes made to the `Gemfile`, the `bundle install` command must be run again so that a new and updated `Gemfile.lock` is created. Otherwise, Bundler will not function properly, and will not install all the necessary dependencies.

**Using Bundler**

To utilize Bundler, add the statement `require 'bundler/setup'` to the beginning of your code file(s). Note that this must be added *before any other required gems* (otherwise these gems will not be added with Bundler). This statement ensures that your program uses what is listed in the `Gemfile.lock` instead of defaulting to the most recent version when loading Gems used by the program.

Note that Bundler does not change at all how Rubies and Gems are stored. This is determined by the Ruby Version Manager.bundle exec

Use the `bundle exec` command directly from the command line when you can't add the `require 'bundler/setup'` statement directly to the code file (such as with the `Rakefile`), or when there are dependency conflicts within the project itself, or between the CLI environment and the project.

**bundle exec**

`bundle exec` ensures that the command you run will execute in an environment that includes the versions outlined in the `Gemfile.lock`. Typically this is used for gems that run directly from the command  line, which may have different versions of ruby and it's gems than those outlined in the program by the `Gemfile.lock`. These can include `rake`, `pry`, etc. Because the shell cannot access the `Gemfile.lock`, we use `bundle exec` to ensure the environment uses to correct version information.

If you see an error message like:

```
Gem::LoadError: You have already activated rake 11.3.0, but your Gemfile requires rake 10.4.2. Prepending `bundle exec` to your command may solve this.
```

You can fix it by running `bundle exec` with the command in question.

**Rake**

A Ruby gem that automates common  and repetitive actions, such as tasks pertaining to building, testing,  packaging and installing programs. Specifically, these can include  setting up an environment (building directories and files), running  tests, common Git tasks, packaging for distribution, as well as any  number of other things.

Rake comes included with all modern Ruby installations, and does not need to be installed.

Define which tasks you want to automate for a particular project by adding a `Rakefile` to the project directory. This file will include the name, description, and actual code behind any of the tasks you want to automate. It is  written in plain Ruby with some specific DSL method calls that pertain  to rake:

- `desc` = gives a short description of the task
- `task` = associates a task name with a block of code (or list of dependencies)

```
desc 'Task description'
task :name do
  # ruby code that implements the task goes here
end
```

Each of the tasks described in the `Rakefile` can be executed from the CLI using the `rake` command + the name of the task in the rakefile (i.e. `rake name`). You can also define a **default** task within the `Rakefile`, which will run if no specific task name is provided to the `rake` command.

```
desc 'description here'
task :default => [ :task_1, :task_2 ]
```

Run the command `rake -T` from the CLI to list all the commands Rake can run along with their associated descriptions.

If your program uses Bundler, you should run the command `bundle exec` with `rake` to ensure that your CLI environment corresponds to the dependencies of your project.