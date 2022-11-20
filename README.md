Full-featured ImageMagick on Ubuntu
==========

This project aims to provide Dockerfile(s) to compile full-featured ImageMagick's executable file with **dynamic-linking** on Ubuntu-based Linux distributions.

#### Why not static?

If someone only uses Ubuntu and have no need to cross compile ImageMagick for other platform, dynamic linking can help re-using a lot of shared libraries and generating smaller and more efficient executable files.

However, this project still uses some static libraries which are useful but not provided by Ubuntu software repositories.

## Getting Start

#### Install Docker

```bash
sudo apt install docker-ce
```

#### Compile

```bash
docker build -t imagemagick-build -f Dockerfile.<ubuntu_name> .
docker run -v "$(pwd)/output":/output --name imagemagick-build imagemagick-build
```

`<ubuntu_name>` can be `Jammy` (22.04).

Now, the executable files should be in the `./output` directory.

#### Clean Up

```bash
docker rm imagemagick-build
docker image rm imagemagick-build && docker image prune
```

## Run ImageMagick's Executable File

1. Open the Dockerfile you used. 
2. Copy the `apt install` command in the runtime environment stage.
3. Run the command in the Ubuntu system that you want to run ImageMagick's executable file (to fix shared libraries not found issues).

#### Are these executable files Debian-compatible?

No. Even though Ubuntu is based on Debian, their software sources are somewhat different. Maybe you can find replaceable packages but I would recommend just modify the base image written in the Dockerfile of this project to a corresponding Debian image and build it.