# TODO: Ruby Dockerfile

FROM ruby:latest AS build

# Make new directory called operator-build and cd
WORKDIR /operator-build

# Copy contents of Gemfile into new operator-build dir
ADD Gemfile .

# configure bundler to write gems to workspace
# RUN bundle config set path workspace
# bundle gems to the workspace folder
# RUN bundle install

RUN BUNDLE_PATH=workspace bundle install

FROM busybox

COPY --from=build /operator-build /operator-build

WORKDIR /operator-build

# inside the workspace/ruby directory, look for a directory type that starts with the name newrelic_rpm
# example, found: workspace/ruby/3.2.0/gems/newrelic_rpm-9.9.0
# -exec: everytime the 'find' is hit, copy recursively each match (is one in this case, workspace/ruby/3.2.0/gems/newrelic_rpm-9.9.0 ) from find into a new directory called instrumentation
RUN sh -c "find 'workspace/ruby/' -type d -name newrelic_rpm\\* -exec cp -r '{}' /instrumentation \\;"

RUN chmod -R go+r /instrumentation

RUN rm -rf /operator-build