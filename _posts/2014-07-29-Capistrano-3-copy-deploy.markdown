---
layout: post
title:  "Capistrano 3 deploy for \":deploy_via, :copy\" orphans"
tags: Ruby Capistrano deploy git
---

Capistrano 2 had a feature that enabled deploy by copying the project tarball to the remote server instead of _git cloning it_ from the remote server, Capistrano 3 doesn't had this feature. The problem of cloning it from the remote server is that sometimes the remote server doesn't have access to the git repository and adding access to it is not desirable.

Just a note, or rant: Capistrano isn't a good example of well documented project and Ruby doesn't have clear semantic on what is public API and what should be considered private API, so I'm not 100% I made a hack or a honest use of their API, this works with Capistrano 3.2.1.

## The code, hack, solution, whatever you call it

In Capistrano 2 times the elders of Google told me that a "set :deploy_via, :copy" should be enough to do the job, with Capistrano 3 Google
just says it's possible with few lines of code, but doesn't say how.

The code bellow is in deploy.rb, hope you understand how it works by reading the comments.

{% highlight ruby %}
# This is important, since the solution was tested only with 3.2.1
lock '3.2.1'

set :application, 'Hello'
# We will tell a white lie to Capistrano
set :scm, :git

# release id is just the commit hash used to create the tarball.
set :project_release_id, `git log --pretty=format:'%h' -n 1 HEAD`
# the same path is used local and remote... just to make things simple for who wrote this.
set :project_tarball_path, "/tmp/#{fetch(:application)}-#{fetch(:project_release_id)}.tar.gz"

# We create a Git Strategy and tell Capistrano to use it, our Git Strategy has a simple rule: Don't use git.
module NoGitStrategy
  def check
    true
  end

  def test
    # Check if the tarball was uploaded.
    test! " [ -f #{fetch(:project_tarball_path)} ] "
  end

  def clone
    true
  end

  def update
    true
  end

  def release
    # Unpack the tarball uploaded by deploy:upload_tarball task.
    context.execute "tar -xf #{fetch(:project_tarball_path)} -C #{release_path}"
    # Remove it just to keep things clean.
    context.execute :rm, fetch(:project_tarball_path)
  end

  def fetch_revision
    # Return the tarball release id, we are using the git hash of HEAD.
    fetch(:project_release_id)
  end
end

# Capistrano will use the module in :git_strategy property to know what to do on some Capistrano operations.
set :git_strategy, NoGitStrategy

# Finally we need a task to create the tarball and upload it,
namespace :deploy do
  desc 'Create and upload project tarball'
  task :upload_tarball do |task, args|
    tarball_path = fetch(:project_tarball_path)
    # This will create a project tarball from HEAD, stashed and not committed changes wont be released.
   `git archive -o #{tarball_path} HEAD`
    raise 'Error creating tarball.'if $? != 0

    on roles(:all) do
      upload! tarball_path, tarball_path
    end
  end
end

# Attach our upload_tarball task to Capistrano deploy task chain.
before 'deploy:updating', 'deploy:upload_tarball'
{% endhighlight %}

This worked for me™.

