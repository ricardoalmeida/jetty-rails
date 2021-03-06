= jetty-rails

http://jetty-rails.rubyforge.net

== DESCRIPTION:

jetty_rails aims to run any Warbler based jruby on rails applications with Jetty Container, loading configuration from Warbler.

This project is useful for people developing jruby on rails apps that can not use mongrel for development. Rails applications integrated with servlet based applications in the same context would be a reasonable reason.

The project has born from my own needs. I needed to run JForum (http://jforum.net) on the same context of my jruby on rails application. I had also to integrate HttpSessions (avoiding single sign on) and use ServletContext in-memory cache store.

== FEATURES:

* Uses {JRuby Rack}[http://wiki.jruby.org/wiki/JRuby_Rack].
* Loads all jars inside your application lib/ dir, by default.
* Loads all classes inside your application classes/ dir, by default.
* Supports rails and merb applications out of the box.

== KNOWN ISSUES

* To generate coverage report with jruby (>= 1.1) follow instructions from http://www.ruby-forum.com/topic/146252 and run (inside jetty-rails root dir):
jruby -S rake rcov

* Hoe in jruby has an issue reading the ~/.hoerc file. Just remove it.

== USAGE:

=== Rails:

  cd myrailsapp
  jruby -S jetty_rails
  
help option shows usage details:
  
  jruby -S jetty_rails --help
  
=== Merb:

  cd mymerbapp
  jruby -S jetty_merb

help option shows usage details:

  jruby -S jetty_merb --help

=== Merb:

  cd mymerbapp
  jruby -S jetty_merb

help option shows usage details:

  jruby -S jetty_merb --help


== REQUIREMENTS:

jetty-rails requires jruby (>=1.1). Please make sure you already have 
it properly installed and inserted in your PATH environment variable.

{Installing JRuby Instructions}[http://wiki.jruby.org/wiki/Getting_Started]

== INSTALL:

  jruby -S gem install jetty-rails
  
== BUGS AND NEW FEATURES

Using Lighthouse: http://fabiokung.lighthouseapp.com/projects/12666-jetty-rails


== MULTIPLE SERVERS:

You can specify a configuration yaml file rather than command line switches. 
The file also allows specifying multiple servers and / or application contexts for single jetty container.

For example, you could set a context_path of /testA on port 8888 which is rails, /testB also that port which is merb.
Or, you could have /testA on port 8888 and /testB on port 9999.

 jruby -S jetty_rails -c path/to/config.yml

The configuration options are inherited, so if you specify the environment to be "production" at the top level, 
then any servers and application context will be "production" unless the choose to override the value.

- server settings:
  <tt>:port</tt>, <tt>:jruby_min_runtimes</tt>, <tt>:jruby_max_runtimes</tt>, <tt>:thread_pool_max</tt>, <tt>:thread_pool_min</tt>, <tt>:acceptor_size</tt>

- application context settings:
  <tt>:context_path</tt>, <tt>:base</tt>, <tt>:adapter</tt>, <tt>:environment</tt>, <tt>:lib_dir</tt>, <tt>:gem_path</tt>

As part of the configuration you have some control over jruby & jetty.

See spec/config.yml, spec/jetty_rails_sample_1.yml, and spec/jetty_rails_sample_2.yml for more examples.

=== Rails:

If -c is not specified, by default jetty_rails will look for a config/jetty_rails.yml relative to where it is started.

Don't forget to add this into your config/environment.rb
ActionController::AbstractRequest.relative_url_root = "/testA"


=== JRuby Configuration

You can tweak the JRuby runtimes per application context:

  jruby_min_runtimes: 1
  jruby_max_runtimes: 2


=== Jetty Configuration

You can also modify the jetty per server configurations:

Thread pool will define the thread pool available to the jetty server using a QueuedThreadPool.

  thread_pool_max: 40
  thread_pool_min: 1


The acceptor size is the number of acceptor threads available for that server's channel connector.

  acceptor_size: 20

See the jetty documentation for more information.


== LICENSE:

Jetty Rails is distributed under the terms of The MIT License.
Copyright (c) 2008 Fabio Kung <fabio.kung@gmail.com>
  
Read more details in the bundled +Licenses.txt+ file. There are other 
pieces of software bundled with jetty-rails. Before using jetty-rails, 
make sure you agree with all of them.
