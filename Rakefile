require 'rake'

desc 'Initializes/updates vim plugins and configuration files'
task default: ['vim:init', 'vim:configure']

$prefix = ENV['HOME'] || '~'
$source = File.expand_path File.dirname(__FILE__)

namespace :vim do
  desc 'Initializes/updates vim bundle plugins'
  task :init do
    cmds = ['git submodule init', 'git submodule update']
    cmds.each { |cmd| sh cmd }
  end

  target_rc = File.join($prefix, '.vimrc')
  source_rc = File.join($source, 'rc', 'vimrc')
  target_bundle = File.join($prefix, '.vim')

  desc 'Configures vim with custom rc and bundles'
  task configure: [target_bundle, target_rc]

  rule target_rc => FileList[source_rc] do
    rm target_rc if File.exist? target_rc
    cp source_rc, target_rc
  end

  rule target_bundle => FileList["#{$source}/vim/**/*"] do |t|
    vim_path = File.join($prefix, '.vim') 
    Dir.mkdir(vim_path) unless Dir.exists?(vim_path)
    rm_r(target_bundle, force: true)
    cp_r("#{$source}/vim/.", target_bundle, remove_destination: true)
  end
end

def cp_overwrite(source, target)
  rm target if File.exist? target
  cp source, target
end

namespace :tmux do

  target = "#{$prefix}/.tmux.conf"
  source = "#{$source}/rc/tmux.conf"

  desc 'Configures tmux'
  task configure: target

  rule target => FileList[source] do
    cp_overwrite source, target
  end
end

namespace :zsh do

  target = "#{$prefix}/.zshrc"
  source = "#{$source}/rc/zshrc"

  desc 'Configures zsh'
  task configure: target

  rule target => FileList[source] do
    cp_overwrite source, target
  end
end
