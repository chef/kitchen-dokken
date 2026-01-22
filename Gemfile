source "https://rubygems.org"

# Specify your gem's dependencies in kitchen-dokken.gemspec
gemspec

# Override transitive dependency on test-kitchen with chef-test-kitchen-enterprise
# The git repo now includes a test-kitchen.gemspec alias to satisfy transitive dependencies
gem "chef-test-kitchen-enterprise", git: "https://github.com/chef/chef-test-kitchen-enterprise", branch: "remove-chef-provisioner", glob: "test-kitchen.gemspec" # TODO: update branch to main once PR is merged https://github.com/chef/chef-test-kitchen-enterprise/pull/60
gem "test-kitchen", git: "https://github.com/chef/chef-test-kitchen-enterprise", branch: "remove-chef-provisioner", glob: "test-kitchen.gemspec" # TODO: update branch to main once PR is merged https://github.com/chef/chef-test-kitchen-enterprise/pull/60
# Check if Artifactory is accessible, otherwise use GitHub
artifactory_url = "https://artifactory-internal.ps.chef.co/artifactory/api/gems/omnibus-gems-local"
artifactory_available = begin
                          require "net/http"
                          require "uri"
                          uri = URI.parse(artifactory_url)
                          http = Net::HTTP.new(uri.host, uri.port)
                          http.use_ssl = true
                          http.open_timeout = 3
                          http.read_timeout = 3
                          response = http.head(uri.path)
                          response.is_a?(Net::HTTPSuccess) || response.is_a?(Net::HTTPRedirection)
                        rescue StandardError
                          false
                        end

if artifactory_available
  source artifactory_url do
    gem "kitchen-chef-enterprise"
  end
else
  gem "kitchen-chef-enterprise", git: "https://github.com/chef/kitchen-chef-enterprise", branch: "main"
end

group :test do
  gem "berkshelf"
  gem "kitchen-inspec"
  gem "inspec-core", ">= 5.0", "< 6.6.0" # Inspec 6.6.0+ requires license key to run, this limits it to pre license key for CI and testing purposes
  gem "rake", ">= 11.0"
end

group :development do
  gem "pry"
  gem "pry-byebug"
end

group :cookstyle do
  gem "cookstyle"
end
