# Docker Shinobi

A docker image built through github action with git commit version tag

# Why

I found that shinobi's docker image is difficult to find. 
The code on [github](https://github.com/ShinobiCCTV/Shinobi) is no longer up to date.
The image on docker [hub](https://hub.docker.com/r/shinobisystems/shinobi) is very old and no ARM support. 

Since shinobi has moved [gitlab](https://gitlab.com/Shinobi-Systems/Shinobi) and published the image to the gitlab [registry](https://gitlab.com/Shinobi-Systems/Shinobi/container_registry), 
it is limited by the gitlab ci build cannot be released in time, and the old image cannot be retained because there is no really version number.

After reviewing the following items

- [silvertoken/shinobi](https://github.com/silvertoken/shinobi)
- [diegosc78/docker-shinobi-arm64](https://github.com/diegosc78/docker-shinobi-arm64)

Will use github action to build and docker hub to publish the image,
and try to keep it as clean without custom configuration file.

# Tags

The images of this project will be published to docker [hub](https://hub.docker.com/r/xiaoyao9184/shinobi).

Since there is no really version number, and each commit cannot be mirrored
it would be a good idea to manually trigger the action and tag it with commit id.

If you want to fixed version and this project does not provide,
you can fork this project and build it your own image.
