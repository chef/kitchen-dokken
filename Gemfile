source "https://rubygems.org"

gemspec

gem "chef-test-kitchen-enterprise", git: "https://github.com/chef/chef-test-kitchen-enterprise", branch: "main"

group :test do
  gem "berkshelf"
  gem "kitchen-inspec"
  gem "rake", ">= 11.0"
end

group :development do
  gem "pry"
end

group :linting do
  gem "cookstyle", "7.32.8"
end
