# Docker Customised Image
## 1 Create a Dockerfile
### Dockerfile Common Content
* from: the image dependency
* copy: copy content to the image
* workdir: declare the default working directory
* cmd: command to execute
  * the command will be executed under the working directory

## 2 Build your image
```sh
docker build -t YOUR_IMAGE_NAME:[YOUR_TAG] .
```