PROJECT_NAME = "ruby-station"

begin
  require 'jeweler'
rescue LoadError
  puts "Jeweler not available. Install it with: sudo gem install technicalpickles-jeweler -s http://gems.github.com"
end

Jeweler::Tasks.new do |gemspec|
  gemspec.name = "#{PROJECT_NAME}"
  gemspec.summary = "Create, Distribute, and Install Ruby applications easily"
  gemspec.email = "yutaka.hara/at/gmail.com"
  gemspec.homepage = "http://github.com/yhara/#{PROJECT_NAME}"
  gemspec.description = gemspec.summary
  gemspec.authors = ["Yutaka HARA"]
  gemspec.add_dependency('ramaze', '>= 2009.07')
  gemspec.add_dependency('dm-core', '~> 1.0.0')
  gemspec.add_dependency('dm-sqlite-adapter', '~> 1.0.0')
  gemspec.add_dependency('dm-migrations', '~> 1.0.0')
  gemspec.add_dependency('json')
  gemspec.add_development_dependency('rspec', '= 1.2.9')
  gemspec.add_development_dependency('cucumber', '= 0.4.2')
  gemspec.add_development_dependency('rack-test', '= 0.5.0')
  gemspec.add_development_dependency('webrat', '= 0.5.3')
  gemspec.add_development_dependency('culerity', '= 0.2.3')
  gemspec.executables = ["ruby-station"]
end

desc "install current source as gem"
task :dogfood => [:gemspec, :build] do
  sh "sudo gem install pkg/#{PROJECT_NAME}-#{File.read("VERSION").chomp}.gem"
end

desc "uninstall the installed gem"
task :undogfood do
  sh "sudo gem uninstall #{PROJECT_NAME}"
end

desc "uninstall, then install current source as gem"
task :redogfood => [:undogfood, :dogfood]

desc "uninstall temporary gem and install from github"
task :nodogfood do
  sh "sudo gem uninstall #{PROJECT_NAME}"
  sh "sudo gem install yhara-#{PROJECT_NAME}"
end

desc "check for gem to be built"
task :stalk do
  sh "gemstalk yhara #{PROJECT_NAME}"
end

# for runtime

runtime_version = File.read("runtime/VERSION").chomp

desc "Create runtime gem"
task :runtime do
  cd "runtime/"
  sh "rake gemspec"
  sh "gem build ruby-station-runtime.gemspec"
end
