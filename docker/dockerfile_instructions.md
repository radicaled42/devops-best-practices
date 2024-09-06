# Dockerfile instructions

| **Instruction** | **Description**                                   |
|-----------------|---------------------------------------------------|
| ADD             | Add local or remote files and directories.        |
| ARG             | Use build-time variables.                         |
| CMD             | Specify default commands.                         |
| COPY            | Copy files and directories.                       |
| ENTRYPOINT      | Specify default executable.                       |
| ENV             | Set environment variables.                        |
| EXPOSE          | Describe which ports your application is listening on. |
| FROM            | Create a new build stage from a base image.       |
| HEALTHCHECK     | Check a container's health on startup.            |
| LABEL           | Add metadata to an image.                         |
| MAINTAINER      | Specify the author of an image.                   |
| ONBUILD         | Specify instructions for when the image is used in a build. |
| RUN             | Execute build commands.                           |
| SHELL           | Set the default shell of an image.                |
| STOPSIGNAL      | Specify the system call signal for exiting a container. |
| USER            | Set user and group ID.                            |
| VOLUME          | Create volume mounts.                             |
| WORKDIR         | Change working directory.                         |

**FROM**

Whenever possible, use current official images as the basis for your images. 

**LABEL**

You can add labels to your image to help organize images by project, record licensing information, to aid in automation, or for other reasons.

**RUN**

Split long or complex RUN statements on multiple lines separated with backslashes to make your Dockerfile more readable, understandable, and maintainable.

**CMD**

The CMD instruction should be used to run the software contained in your image, along with any arguments. CMD should almost always be used in the form of CMD ["executable", "param1", "param2"]. 

**ENTRYPOINT**

The best use for ENTRYPOINT is to set the image's main command, allowing that image to be run as though it was that command, and then use CMD as the default flags.

**Use ENTRYPOINT when you want to define a command that always runs.
Use CMD to provide default arguments to ENTRYPOINT or to specify a default command if ENTRYPOINT is not used.**

**EXPOSE**

The EXPOSE instruction indicates the ports on which a container listens for connections. Consequently, you should use the common, traditional port for your application.

**ENV**

To make new software easier to run, you can use ENV to update the PATH environment variable for the software your container installs.

**ADD or COPY**

ADD and COPY are functionally similar. COPY supports basic copying of files into the container, from the build context or from a stage in a multi-stage build. ADD supports features for fetching files from remote HTTPS and Git URLs, and extracting tar files automatically when adding files from the build context.


**VOLUME**

You should use the VOLUME instruction to expose any database storage area, configuration storage, or files and folders created by your Docker container. You are strongly encouraged to use VOLUME for any combination of mutable or user-serviceable parts of your image.

**USER**

If a service can run without privileges, use USER to change to a non-root user.

**WORKDIR**

For clarity and reliability, you should always use absolute paths for your WORKDIR. 

**ONBUILD**

An ONBUILD command executes after the current Dockerfile build completes. ONBUILD executes in any child image derived FROM the current image. Think of the ONBUILD command as an instruction that the parent Dockerfile gives to the child Dockerfile.

## Bibliography
- https://docs.docker.com/build/building/best-practices/#dockerfile-instructions
- https://docs.docker.com/reference/dockerfile/