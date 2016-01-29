# vim:ft=ruby

source ENV['GEM_SOURCE'] || "https://rubygems.org"

def location_for(place, version = nil)
  if place =~ /^(git[:@][^#]*)#(.*)/
    [version, { :git => $1, :branch => $2, :require => false}].compact
  elsif place =~ /^file:\/\/(.*)/
    ['>= 0', { :path => File.expand_path($1), :require => false}]
  else
    [place, version, { :require => false}].compact
  end
end

group :development, :unit_tests do
  gem 'rspec-puppet', '~> 2.1',  :require => false
  gem 'rspec-core', '3.1.7',     :require => false
  gem 'puppetlabs_spec_helper',  :require => false
  gem 'simplecov',               :require => false
  gem 'puppet_facts',            :require => false
  gem 'json',                    :require => false
end
group :system_tests do
  gem 'beaker-rspec',  :require => false
  gem 'serverspec',    :require => false
end

gem 'facter', *location_for(ENV['FACTER_GEM_VERSION'])
gem 'puppet', *location_for(ENV['PUPPET_GEM_VERSION'])


if File.exists? "#{__FILE__}.local"
  eval(File.read("#{__FILE__}.local"), binding)
end
