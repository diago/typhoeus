$LOAD_PATH.unshift(File.dirname(__FILE__))

require "lib/typhoeus/version"

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gemspec|
    gemspec.name = "typhoeus"
    gemspec.summary = "A library for interacting with web services (and building SOAs) at blinding speed."
    gemspec.description = "Like a modern code version of the mythical beast with 100 serpent heads, Typhoeus runs HTTP requests in parallel while cleanly encapsulating handling logic."
    gemspec.email = "dbalatero@gmail.com"
    gemspec.homepage = "http://github.com/dbalatero/typhoeus"
    gemspec.authors = ["Paul Dix", "David Balatero"]
    gemspec.add_dependency "mime-types"
    gemspec.add_development_dependency "rspec", "~> 2.6"
    gemspec.add_development_dependency "jeweler"
    gemspec.add_development_dependency "diff-lcs"
    gemspec.add_development_dependency "sinatra"
    gemspec.add_development_dependency "json"
  end

  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler not available. Install it with: gem install jeweler"
end

require 'rspec/core/rake_task'
RSpec::Core::RakeTask.new do |t|
end

task :install do
  rm_rf "*.gem"
  puts `gem build typhoeus.gemspec`
  puts `gem install typhoeus-#{Typhoeus::VERSION}.gem`
end

desc "Builds the native code"
task :build_native do
  system("cd ext/typhoeus && ruby extconf.rb && make")
end

desc "Start up the test servers"
task :start_test_servers do
  puts "Starting 3 test servers"
  (3000..3002).map do |port|
    Thread.new do
      system("ruby spec/servers/app.rb -p #{port}")
    end
  end.each(&:join)
end

desc "Run all the tests"
task :default => :spec
