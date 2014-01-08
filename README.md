# Buildstep

Heroku-style application builds using Docker and Buildpacks. Used by [Dokku](https://github.com/progrium/dokku) to make a mini-Heroku.

## Requirements

 * Docker
 * Git
 * buildstep-capistrano (https://github.com/kyuss/heroku-buildpack-capistrano)
 
## Building Buildstep

The buildstep script uses a buildstep base container that needs to be built. It must be created before
you can use the buildstep script. To create it, run:

    $ make build

This will create a container called `progrium/buildstep` that contains all supported buildpacks and the
builder script that will actually perform the build using the buildpacks.

## Building an App

Running the buildstep script will take an application tar via STDIN and an application container name as
an argument. It will put the application in a new container based on `progrium/buildstep` with the specified name. 
Then it runs the builder script inside the container. 

    $ cat myapp.tar | ./buildstep myapp

The resulting container has a built app ready to go. The builder script also parses the Procfile and produces
a starter script that takes a process type. Run your app with:

    $ docker run -d myapp /bin/bash -c "/exec cap deploy"

## License

MIT
