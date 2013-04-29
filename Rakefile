def __DIR__
  File.expand_path('..', __FILE__)
end

desc 'Build presentation'
task :build do
  sh %{slideshow --h2 --output output --template reveal.js --config #{__DIR__} presentation.text}
  sh %{cp presentation.text output/presentation.txt}
end

require 'tmpdir'
desc 'Deploy to gh-pages'
task :deploy => [:build] do

  Dir.mktmpdir do |tmp|
    commands = <<-EOS
      git init --reference #{__DIR__} git@github.com:adrienthebo/puppet-modules-presentation"
      git checkout -b gh-pages origin/gh-pages
      cp -r #{__DIR__}/output/* #{tmp}/
      cd #{tmp}
      git add .
      git ci -a -m 'gh-pages update via rake task'
      git push
      cd
      rm -rf #{tmp}"
    EOS

    commands.split("\n").each {|ell| sh ell.strip}
  end
end

task :default => :build
