require 'environment'
require 'spec/rake/spectask'

task :default => :test
task :test => :spec

if !defined?(Spec)
  puts "spec targets require RSpec"
else
  desc "Run all examples"
  Spec::Rake::SpecTask.new('spec') do |t|
    t.spec_files = FileList['spec/**/*.rb']
    t.spec_opts = ['-cfs']
  end
end

namespace :db do
  desc 'Auto-migrate the database (destroys data)'
  task :migrate do
    DataMapper.auto_migrate!
  end

  desc 'Auto-upgrade the database (preserves data)'
  task :upgrade do
    DataMapper.auto_upgrade!
  end
end

namespace :twitter do
  desc 'Update the local status cache'
  task :update do
    count = Status.update
    puts "#{count} new status updates retrieved"
  end
end

# Rake task to install required gem dependencies
namespace :gems do
  desc 'Install Required Gems'
  task :install do
    required_gems = %w{ sinatra dm-core dm-validations 
                        dm-aggregates haml twitter rspec_hpricot_matchers }
    required_gems.each {|required_gem| system "sudo gem install #{required_gem}" }
  end
end
