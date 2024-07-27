GitLab CI templates

Templating with hidden keys
Jobs defined with a leading period (.) are disregarded, rendering .template incapable of specifying active and executable tasks. This functionality is termed hidden keys.
YAML permits the referencing of its own segments to prevent redundant copying and pasting, effectively minimizing code. This capability is known as an "anchor."

.template: &template
Where &template is an alias that we can provide to the .template job
When using "<<: *template,
" we are instructing to replicate all actions defined in the job template. If there is a need to modify certain keys already present in the template, it is necessary to explicitly redefine those keys.
example:
stages:
- build
- test
.docker_template: &template
tags:
- CI
- Devops
rules:
- if: $CI_COMMIT_BRANCH == "main"
timeout: 1 hours 30 minutes
docker_build_job:
<<: *template
stage : build
script:
- echo “Build Started”
docker_test_job:
<<: *template
stage : test
script:
- echo “Test Started”
#template

Or we can use extend to do the same 
Example
GitLab CI - extends We can use extends to reuse the configuration section
.tests:
image: httpd
script: “
./test.sh”
stage: test
timeout: 10m
test_job:
extends: .tests
script: “
./new.sh”
#extends
Example
Thanks !!
