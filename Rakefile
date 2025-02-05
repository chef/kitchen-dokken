require "bundler/gem_tasks"
require "cookstyle"
require "rubocop/rake_task"

RuboCop::RakeTask.new(:style) do |task|
  task.options += ["--display-cop-names", "--no-color"]
end

task default: %i{style}
