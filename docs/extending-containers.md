# Extending Containers
To add a container, the class file must be located in [`lib/java_buildpack/container`][container_dir] and the class name added to [`config/components.yml`][components_yml].  The class must have the following methods

[container_dir]: ../lib/java_buildpack/container
[components_yml]: ../config/components.yml

```ruby
# An initializer for the instance.
#
# @param [Hash<Symbol, String>] context A shared context provided to all components
# @option context [String] :app_dir the directory that the application exists in
# @option context [String] :java_home the directory that acts as +JAVA_HOME+
# @option context [Array<String>] :java_opts an array that Java options can be added to
# @option context [String] :lib_directory the directory that additional libraries are placed in
# @option context [Hash] :configuration the configuration provided by the user
def initialize(context)

# Determines if the container can be used to run the application.
#
# @return [Array<String>, String, nil] If the container can be used to run the application, a +String+ or an
#                                      +Array<String>+ that uniquely identifies the container (e.g.
#                                      +tomcat-7.0.29+).  Otherwise, +nil+.
def detect

# Downloads and unpacks the container.  The container is expected to transform the application in whatever way
# necessary (e.g. moving files or creating symbolic links) to run it.  Status output written to +STDOUT+ is expected as
# part of this invocation.
#
# @return [void]
def compile

# Creates the command to run the application with.  The container is expected to read +context[:java_home]+ and
# +context[:java_opts]+ and take those values into account when creating the command.
#
# @return [String] the command to run the application with
def release
```