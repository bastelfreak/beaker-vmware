source ENV['GEM_SOURCE'] || "https://rubygems.org"

gemspec



def location_for(place, fake_version = nil)
  if place =~ /^git:([^#]*)#(.*)/
    [fake_version, { :git => $1, :branch => $2, :require => false }].compact
  elsif place =~ /^file:\/\/(.*)/
    ['>= 0', { :path => File.expand_path($1), :require => false }]
  else
    [place, { :require => false }]
  end
end


# We don't put beaker in as a test dependency because we
# don't want to create a transitive dependency
group :acceptance_testing do
  gem "beaker", *location_for(ENV['BEAKER_VERSION'] || '>= 3.0')
end

group :release do
  gem 'github_changelog_generator', require: false
end

group :coverage, optional: ENV['COVERAGE']!='yes' do
  gem 'simplecov-console', :require => false
  gem 'codecov', :require => false
end
