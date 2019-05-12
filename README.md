# vyos-build-crux

based on https://pgfitzgerald.wordpress.com/2019/02/11/how-to-build-a-vyos-1-2-0-iso-image/

I used this container to successfully make 1.2.0 and 1.2.1 ISOs that are now working in production env. 

# Run the VyOS Build Container

Now that we have the build container, let’s run it. The –rm parameter instructs Docker to remove the container when we exit. The -it parameter instructs Docker to run the container interactively. The –privileged parameter instructs Docker to run the container with (almost) all the capabilities of the host machine. The -v $(pwd):/vyos parameter instructs Docker to mount the current working directory on the host as /vyos within the container. The -w /vyos parameter instructs Docker to set /vyos as the current working directory within the container. The vyos-builder parameter just tells Docker to run the container image tagged with that value. And finally, the bash parameter instructs Docker to execute the bash command so you’ll have a shell to work with.

```curl -O -L https://github.com/vyos/vyos-build/archive/crux.zip``` ```

yum install unzip

unzip crux.zip

cd vyos-build-crux

docker run --rm -it --privileged -v $(pwd):/vyos -w /vyos milekz/vyos-build-crux bash```

# Configure the Build

Now that the container is running, you should be at a prompt that looks something like this:

root@efa0ecf8a19d:/vyos#

You should already be in the right directory, so configuring the build is as easy as executing the following command.

```./configure --architecture amd64 --build-by "your@email.eu" --build-type release --version 1.2.1```

Build the ISO Image

Now, for the payoff! The following command will build the ISO image. This will also take a while, so top off that coffee and take another break.

```make iso```

You’re Done!

You should have a brand spanking new ISO image in the build directory.
