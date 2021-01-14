# Deploy node.js app on Docker container using Jenkins

Pre-requisites:
1. Setup Jenkins server and install required plugins
1. Setup pipeline job add use Jenkinsfile for the same
1. Setup a target server which running with Docker service


`Jenkinsfile:` - This file contains instructions to build node.js application. Once build stage completed it copy artifacts onto target server (which runs with Docker) and create image and container there.
`Dockerfile:` - Dockerfile should exist on target server where we copy artifacts. this is going to create image using the artifacts which copied by the Jenkins (Deploy stage)
`server.js and package.json:` - A simple "hello world" node.js application
