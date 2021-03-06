require 'rubygems'
gem 'hoe', '>= 2.1.0'
require 'hoe'
require 'fileutils'
require File.dirname(__FILE__) + '/lib/daemon_kit'

Hoe.plugin :newgem
Hoe.plugin :website
# Hoe.plugin :cucumberfeatures

# Generate all the Rake tasks
# Run 'rake -T' to see list of generated tasks (from gem root directory)
$hoe = Hoe.spec('daemon-kit') do |p|
  p.summary = 'Daemon Kit aims to simplify creating Ruby daemons by providing a sound application skeleton (through a generator), task specific generators (jabber bot, etc) and robust environment management code.'
  p.developer('Kenneth Kalmer', 'kenneth.kalmer@gmail.com')
  p.changes              = p.paragraphs_of("History.txt", 0..1).join("\n\n")
  p.post_install_message = IO.read( 'PostInstall.txt' ) # TODO remove if post-install message not required
  p.rubyforge_name       = 'kit' # TODO this is default value
  p.extra_deps = [
                  ['rubigen', '>= 1.5.2'],
                  ['eventmachine', '>=0.12.8']
                 ]
  p.extra_dev_deps = [
                      ['newgem', ">= #{::Newgem::VERSION}"]
                     ]

  p.clean_globs |= %w[**/.DS_Store tmp *.log]
  path = (p.rubyforge_name == p.name) ? p.rubyforge_name : "\#{p.rubyforge_name}/\#{p.name}"
  p.remote_rdoc_dir = File.join(path.gsub(/^#{p.rubyforge_name}\/?/,''), 'rdoc')
  p.rsync_args = '-av --delete --ignore-errors'
end

require 'newgem/tasks' # load /tasks/*.rake
Dir['tasks/**/*.rake'].each { |t| load t }

# TODO - want other tests/tasks run by default? Add them to the list
task :default => [:spec] #, :features]
