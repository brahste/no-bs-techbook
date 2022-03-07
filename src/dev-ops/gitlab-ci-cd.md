# Understanding GitLab CI/CD

pipelines automate a series of steps or stages such as initiating code builds, running tests, deploying and staging environments.

This starts with a code _commit_, afgter the commit tests are conducted code quality checkers can be done here and unit tests, next is _build_ once the ocde is tested and integrated the code need to be built, next the _Testing_ stage, this stage checks the intergaction between builds and ensures the app is working correctly, last is the _deploy_ stage where the code is deployed to production. 

What you need to use Git Lac CI/CD:
1. Git codebase
2. Sequentiually defined scripts in a YAML file
3. YAML file in the root path of your repo
4. the file must be named `.gitlab-ci.yml`

In `gitlab-ci.yml` you can define scripts to run, define include and cache dependencies, where you want to deploy application, etc. This file determines the structure of the pipeline, what steps to execute, and make decisions on conditions

How to write a YAML file for CI/CD in gitlab 

- Define your stages: build, test, deploy, etc.
- Define your image
- Define the elements of the various stages in sequence... everything in this `.gitlab-ci.yml` is run in sequence.


