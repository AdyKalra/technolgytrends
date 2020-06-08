# fundamentals which drives a CI/CD pipeline
## Integration and Verification 
* In a typical software development setup you expect multiple developers to be developing in their own **feature branches which they periodically integrate to a common development branch.** 
* When a piece of code is integrated (or even before it’s integrated) , it is essential that a verification step is available that can quickly ensure that the particular integration would not break existing functionality, would not degrade performance or even would not introduce security loopholes.

## Automation 
* In-order to achieve speed, it is essential that verification is automated. i.e. this should be comprised of series of automated tests that would cover most critical aspects of the software and could be executed in a reasonable period of time.

## DevOps culture 
* The development team has a big role to play in ensuring the continuity of the pipeline. For example what happens when a build fails or test fails?. Fixing such issues should take top priority or otherwise it will diminish the returns of the CI/CD process.
## Containerisation 
* not mandatory but if the deployment is based on containers, it will reduce the complexity.

### Tech stack
* Jenkins in master-slave mode as the build server
* Jenkins Pipelines to drive the CI process
* Git Hooks to trigger builds with code commits
* SonarQube as the code quality tool
* Robot Framework for automating functional tests
* JMeter for performance testing
* OWASP ZAP for security scanning

* With Jenkins
  * you'll only need to enable Pipelines and define your workflows to be able to run tests and deployments on your branches.
  * Step 1: Start with a default pipelines to be run on feature branches
  * Step 2: Add a new pipeline for the master branch
  * Step 3: Protect your release branches
  * Step 4: Use pull request to promote changes to production

![CICD](https://miro.medium.com/max/1400/1*-BziHNWo19nQ_edSiO6y0g.png)

## Applications Deployment
![applications_deployment](https://opensource.com/sites/default/files/uploads/applications_deploymentpipeline.png)\

![Version Control](https://opensource.com/sites/default/files/uploads/version-control.png)

![Testing Pyramid](https://opensource.com/sites/default/files/uploads/testing.png)

## Test Env
![CI](https://wac-cdn.atlassian.com/dam/jcr:25127c2f-a53c-4e57-a4ba-3e89c704e508/part-1-v2@2x.png?cdnVersion=1058)
## Staging 
![Staging](https://wac-cdn.atlassian.com/dam/jcr:4f991401-bf02-4bf8-b67d-c9e3072c8d09/part-2-v2@2x.png?cdnVersion=1058)
## Production
![Production](https://wac-cdn.atlassian.com/dam/jcr:84dbe552-eda9-495e-977b-e84ff096781d/part-3-v2@2x.png?cdnVersion=1058)

## CI CD with K8S
![k8s](https://cdn.thenewstack.io/media/2018/07/d00605db-c1cdpiplin.png)
