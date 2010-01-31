require 'rake'
require 'spec/rake/spectask'


desc 'Default: run specs.'
task :default => :spec

desc 'Run the specs'
Spec::Rake::SpecTask.new(:spec) do |t|
  t.spec_opts = ['--colour --format progress --loadby mtime --reverse']
  t.spec_files = FileList['spec/**/*_spec.rb']
end

Spec::Rake::SpecTask.new(:rcov) do |spec|
  spec.libs << 'lib' << 'spec'
  spec.pattern = 'spec/**/*_spec.rb'
  spec.rcov = true
end

begin
  require 'metric_fu'
  MetricFu::Configuration.run do |config|
    config.metrics  = [:saikuro, :flog, :flay, :reek, :roodi, :rcov]
    config.graphs   = [:flog, :flay, :reek, :roodi, :rcov]
    #config.flay     = { :dirs_to_flay => ['app', 'lib'],
                        #:minimum_score => 100  }
    #config.flog     = { :dirs_to_flog => ['app', 'lib']  }
    #config.reek     = { :dirs_to_reek => ['app', 'lib']  }
    #config.roodi    = { :dirs_to_roodi => ['app', 'lib'] }
    #config.saikuro  = { :output_directory => 'scratch_directory/saikuro', 
                        #:input_directory => ['app', 'lib'],
                        #:cyclo => "",
                        #:filter_cyclo => "0",
                        #:warn_cyclo => "5",
                        #:error_cyclo => "7",
                        #:formater => "text"} #this needs to be set to "text"
    #config.churn    = { :start_date => "1 year ago", :minimum_churn_count => 10}
    config.rcov     = { :environment => 'test',
                        :test_files => ['spec/**/*_spec.rb'],
                        :rcov_opts => ["--sort coverage",
                                       #"--no-html",
                                       "--text-coverage",
                                       #"--no-color",
                                       "--profile",
                                       #"--rails",
                                       "--exclude /gems/,/Library/"]}
    config.graph_engine = :bluff
  end
rescue LoadError
  puts "Install metric_fu to run code metrics"
end


begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "truncate_html"
    gem.summary = %Q{Uses an API similar to Rails' truncate helper to truncate HTML and close any lingering open tags.}
    gem.description = %Q{Truncates html so you don't have to}
    gem.email = "harold.gimenez@gmail.com"
    gem.homepage = "http://github.com/hgimenez/truncate_html"
    gem.authors = ["hgimenez"]
    # gem is a Gem::Specification... see http://www.rubygems.org/read/chapter/20 for additional settings
  end
  Jeweler::GemcutterTasks.new

rescue LoadError
  puts "Jeweler (or a dependency) not available. Install it with: sudo gem install jeweler"
end


