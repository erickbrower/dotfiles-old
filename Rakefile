require 'rake'

task default: ['vim:install', 'zsh:install', 'tmux:install']

$prefix = ENV['HOME'] || '~'
$source = File.expand_path File.dirname(__FILE__)

target_zshrc = "#{$prefix}/.zshrc"
source_zshrc = "#{$source}/rc/zshrc"

def cp_overwrite(source, target)
  rm target if File.exist? target
  cp source, target
end

namespace :vim do

  target_rc = "#{$prefix}/.vimrc"
  source_rc = "#{$source}/rc/vimrc"
  target_bundle = "#{$prefix}/.vim"
  source_bundle = "#{$source}/vim/*"

  desc 'Configures vim with custom rc and bundles'
  task install: [target_bundle, target_rc]

  rule target_rc => FileList[source_rc] do
    rm target_rc if File.exist? target_rc
    cp source_rc, target_rc
  end

  rule target_bundle => FileList[source_bundle] do
    cp_r source_bundle, target_bundle, remove_destination: true
  end
end

namespace :tmux do

  target = "#{$prefix}/.tmux.conf"
  source = "#{$source}/rc/tmux.conf"

  desc 'Configures tmux'
  task install: target

  rule target => FileList[source] do
    cp_overwrite source, target
  end
end

namespace :zsh do

  target = "#{$prefix}/.zshrc"
  source = "#{$source}/rc/zshrc"

  desc 'Configures zsh'
  task install: target

  rule target => source do
    cp_overwrite source, target
  end
end
