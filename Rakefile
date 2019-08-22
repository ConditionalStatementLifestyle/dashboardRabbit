# Add your own tasks in files placed in lib/tasks ending in .rake,
# for example lib/tasks/capistrano.rake, and they will automatically be available to Rake.

require_relative 'config/application'
require 'sneakers/tasks'

namespace :rabbitmq do
    desc "Setup routing"
    task :setup do
      require "bunny"
  
      conn = Bunny.new
      conn.start
  
      ch = conn.create_channel
  
      # get or create exchange
      x = ch.fanout("blog.posts")
  
      # get or create queue (note the durable setting)
      queue = ch.queue("dashboard.posts", durable: true)
  
      # bind queue to exchange
      queue.bind("blog.posts")
  
      conn.close
    end
  end
  
Rails.application.load_tasks
