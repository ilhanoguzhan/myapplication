set :application, "myapplication"
set :repository, "git@github.com:ilhanoguzhan/myapplication.git"

set :scm, 'git'

set :admin_runner, "deploy"
set :branch, "master"
set :git_shallow_clone, 1
set :use_sudo, false
set :deploy_to, "/path/public/#{application}"
set :deloy_via, :remote_cache
set :keep_releases, 1
set :rails_env, "production"
set :migrate_target, :latest

default_run_options[:pty] = true
ssh_options[:forward_agent] = true


role :web, "23.21.125.184" # Your HTTP server, Apache/etc
role :app, "23.21.125.184" # This may be the same as your `Web` server
role :db, "23.21.125.184", :primary => true # This is where Rails migrations will run


 namespace :deploy do
   task :start do ; end
   task :stop do ; end
   task :restart, :roles => :app, :except => { :no_release => true } do
     run "#{try_sudo} touch #{File.join(current_path,'tmp','restart.txt')}"
   end
 end

 namespace :deploy do
  task :setup, :except => { :no_release => true } do
    dirs = [deploy_to, releases_path, shared_path]
    dirs += shared_children.map { |d| File.join(shared_path, d.split('/').last) }
    run "mkdir -p #{dirs.join(' ')}"
    run "chmod g+w #{dirs.join(' ')}" if fetch(:group_writable, true)
  end
end
