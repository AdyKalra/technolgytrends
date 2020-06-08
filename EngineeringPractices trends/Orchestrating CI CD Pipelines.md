# CI
* **Continuous Integration (CI) is a development practice that requires developers to integrate code into a shared repository several times a day. Each check-in is then verified by an automated build, allowing teams to detect problems early.**
* Continuous Integration doesn’t get rid of bugs, but it does make them dramatically easier to find and remove.

## If you want to practice CI, the steps roughly go like this:

1. Developers check out code from the repository to work on it locally. Ideally, they create a new branch for the feature they want to implement.
2. When their feature branch is ready, they run tests locally in their development environments.
3. Once all tests pass, they push the commits to the single source repository.
4. Whenever there are changes on the repository, a CI server checks out the changes and performs a “build and test.” A build and test is when the CI server builds the entire system on the developer’s feature branch and runs all the unit and integration tests.
5. The CI server notifies the team of the integration result. There should generally be four outcomes: failed build, successful build, failed tests, successful tests.
6. If there’s a failure, the team fixes the issue ASAP.
7. When the feature branch is merged to the main branch, they repeat steps 2–6.
8. They continue to develop and repeat the steps 2–6 whenever there’s new code to be checked in to the repository.

## The main principles of CI are that you:

1. Check in code in frequently.
2. Automate the build and test portion.
3. Always test the code locally before checking it in.
4. Never merge any failed branches to the main branch.
5. Return its status back to successful if you’re the developer who causes the failed build or test.
6. Make it your top priority to do so once the fail happens

# CD
* **Continuous Deployment is closely related to Continuous Integration and refers to the release into production of software that passes the automated tests.**

# Fundamentals which drives a CI/CD pipeline
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

## BuildPipeline
![BuildPipeline](https://www.afor.co.nz/img/common/BuildPipeline.png)
## CI CD Overview
![cicd-overview](https://www.mendix.com/evaluation-guide/app-lifecycle/attachments/cicd-overview.png)
## CI CD with K8S
![k8s](https://cdn.thenewstack.io/media/2018/07/d00605db-c1cdpiplin.png)
