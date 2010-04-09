require 'rake'
require 'erb'

HOME        = ENV['HOME']
CURRENT_DIR = Dir.pwd
BASH_DIR    = HOME + "/Bash"

desc "Installs Environment on this machine."
task :install do
  # Creates Bash Directory in $HOME
  %x(mkdir -p #{BASH_DIR}/dotfiles #{BASH_DIR}/bin)
  
  # Copy Bashrc file
  %x(cp "#{CURRENT_DIR}/bashrc" "#{BASH_DIR}/bashrc")
  
  # Copy all dotfiles
  Dir.open("#{CURRENT_DIR}/dotfiles").each do |file|
    unless File.directory?("#{CURRENT_DIR}/dotfiles/#{file}")
      %x(cp #{CURRENT_DIR}/dotfiles/#{file} #{BASH_DIR}/dotfiles/#{file})
    end
  end
  
  # Copy all binfiles
  Dir.open("#{CURRENT_DIR}/bin").each do |file|
    unless File.directory?("#{CURRENT_DIR}/bin/#{file}")
      %x(cp #{CURRENT_DIR}/bin/#{file} #{BASH_DIR}/bin/#{file})
    end
  end
  
  # Installs Custom .gemrc file
  %x(cp #{CURRENT_DIR}/gemrc #{HOME}/.gemrc)
  
  # Backup the current ~/.profile if it exists
  if File.exist?("#{HOME}/.profile")
    %x(mv #{HOME}/.profile #{HOME}/.profile.backup.#{Time.now.strftime("%Y-%m-%d-%H-%M-%S")})
  end
  
  # Append the Bash source to the .profile in the $HOME directory
  File.open("#{HOME}/.profile", "w") { |file| file << 'source ~/Bash/bashrc' }

  # Tell user to reload the shell configuration
  puts "\n\nInstalled! Now run the following command to reload the configuration:"
  puts "source ~/.profile\n\n"
end