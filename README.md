#Guard::RemoteSync [![Build Status](https://secure.travis-ci.org/pmcjury/guard-remote-sync.png)](http://travis-ci.org/pmcjury/guard-remote-sync)

## Install
Please be sure to have [Guard](https://github.com/guard/guard) installed before continue.

Install the gem:

```
$ gem install guard-remote-sync
```

Add guard definition to your Guardfile by running this command:

```
$ guard init rspec
```

## Usage

Please read [Guard usage doc](https://github.com/guard/guard#readme)

## Guardfile

RSpec guard can be really adapted to all kind of projects.

### Any directory you need to rsync

```ruby
guard 'remote-sync',
        :source => ".", 
        :destination => '/export/home/{username}/tmp', 
        :user => '{user}',
        :remote_address => '{address}',
        :verbose => true, 
        :cli => "--color", 
        :sync_on_start => true do
  
  watch(%r{^.+\.(js|xml|php|class|config)$})
end
```
Please read [Guard doc](https://github.com/guard/guard#readme) for more information about the Guardfile DSL.

## Options

### There are only two required options

```ruby
guard 'remote-sync', :source => ".", :destination => "./tmp" do
        # ...
end
```

### Syncing to a remote machine required additional options
```ruby
guard 'remote-sync', 
        :source => "."                      # the directory to start the remote sync guard in
        :destination => "/export/home/user  # the directory to sync to
        :user => "someone"                  # the user to user ex: {USER}@somehost.com
        :remote_address => "company.com"    # the remote address ip or url
        do
                # ...
end
```

### Using your own rsync command. This bypasses all validations, etc.
```ruby
guard 'remote-sync', :cli_options => "rsync -Carv . user@company.com:/export/home/user do
        # ...
end
```

### List of available options:

Most of these options are human readable and correspond to rsync's options. Long options are used wherever
possible to be more verbose

```ruby
:source => nil                      # the source directory to start in
:destination => nil                 # the directory to sync to
:user => nil                        # the user to use if remote syncing to another machine
:remote_address => nil              # the remote address to the other machine ip|url
:ssh => false                       # see rsync options : "$ man rsync"
:cli_options => nil                 # used if you want to pass your own rsyn command
:archive => true                    # see rsync options : "$ man rsync"
:recursive => true                  # see rsync options : "$ man rsync"
:verbose => true                    # see rsync options : "$ man rsync"
:delete => true                     # see rsync options : "$ man rsync"
:include => nil                     # see rsync options : "$ man rsync"
:include_from => nil                # see rsync options : "$ man rsync"
:exclude => nil                     # see rsync options : "$ man rsync"
:exclude_from => ".rsync-filter"    # see rsync options : "$ man rsync"
:progress => true                   # see rsync options : "$ man rsync"
:sync_on_start => false             # rsycn when the guard starts instead of waiting for a watcher to trigger guard
:dry_run => false                   # see rsync options : "$ man rsync"
:cvs_exclude => true                # see rsync options : "$ man rsync"
:password_file => nil               # see rsync options : "$ man rsync"
:timeout => 10                      # see rsync options : "$ man rsync"
```

Development
-----------

Pull requests are very welcome! Make sure your patches are well tested. Please create a topic branch for every separate change
you make.

Testing
-------

Please run `bundle exec rake spec`

Author
------

[Patrick H. McJury](https://github.com/pmcjury)
