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

This project will use github action and Docker Hub build and publish images,
and try to keep it as clean without custom configuration file.

# Tags

The images of this project will be published to Docker Hub [xiaoyao9184/shinobi](https://hub.docker.com/r/xiaoyao9184/shinobi).

Since there is no really version number, and cannot create a image for each commit,
so an good idea use manually trigger the action and tag it with commit id.
See [this](https://damienaicheh.github.io/github/actions/2022/01/20/set-dynamic-parameters-github-workflows-en.html) article for more details.

Default image name format is `${DOCKER_USERNAME}/${image_name}`,
the `image_name` filled in when you manually trigger the action.

Default image tag format is `${BRANCH_PREFIX}${ARCH_TYPE}${NO_DB_SUFIX}`, 
Very similar with [official](https://gitlab.com/Shinobi-Systems/Shinobi/-/blob/0aef86bdf443381250eda82567ba56940fd1d99b/.gitlab-ci.yml#L13-L10).
`BRANCH_PREFIX` same as `commit_id` filled in when you manually trigger the action,
`ARCH_TYPE` only allowed `-amd64` or `-nvidia` or `-arm32v7` or `-arm64v8`,
`NO_DB_SUFIX` only allowed `-no-db` or ``,

like this, each tag only support one platform:

| Tag | Platforms |
| ----- | ----- |
| master-amd64 | linux/amd64 |
| master-amd64-no-db | linux/amd64 |
| master-arm32v7 | linux/arm/v7 |
| master-arm32v7-no-db | linux/arm/v7 |
| master-arm64v8 | linux/arm64 |
| master-arm64v8-no-db | linux/arm64 |
| master-nvidia | linux/amd64 |
| master-nvidia-no-db | linux/amd64 |

Two special tags merge multiple platforms:

| Tag | Sameas | Platforms |
| ----- | ----- | ----- |
| master   | master-amd64 | linux/amd64 |
| | master-arm32v7 | linux/arm/v7 |
| | master-arm64v8 | linux/arm64 |
| master-no-db   | master-amd64-no-db | linux/amd64 |
| | master-arm32v7-no-db | linux/arm/v7 |
| | master-arm64v8-no-db | linux/arm64 |

If you want to fixed version and this project does not provide,
you can fork this project and build it your own image.
You need to set two repository variables,
`DOCKERHUB_USERNAME` and `DOCKERHUB_TOKEN`. see [this](https://github.com/docker/login-action#docker-hub)
