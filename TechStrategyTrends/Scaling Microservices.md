# Scaling Microservices

## Use a container-based pipeline: 
* If a pipeline is containerized, you can run it independently with different language versions. 
* “shared libraries are not the solution,” as they create version-specific conflicts. 
* Using a Docker image is better than shared libraries because users can self-serve images with whatever version they want.
* There are many resources on Docker Hub to ease common CI/CD steps such as building a Docker image, git clone, running unit tests, linting projects and security scanning. Using these images can help avoid wasted development effort.

## Consolidate to a single pipeline that operates with context: 
* Instead of managing thousands of pipelines for all your microservices, you use a single malleable pipeline for all integrations and deployments. 
* This method involves Triggers, which carry information to direct actions. In this setup, Triggers carry context, or metadata, allowing a pipeline to change its behavior accordingly. 
* These Triggers could be time-based or centered around actions like a repo Git commit, or pushing a new image. 
* When a trigger is initiated, the trigger brings in relevant dependencies to perform an action, such as cloning a repository or cloning a codebase. Further steps can then consume these unique criteria.

## Adopt canary release testing: 
* If an organization has hundreds or thousands of microservices, spinning up each microservice to run independent tests can quickly become cost-prohibitive. 
* “testing early becomes less useful as infrastructure complexity arises.”
* To solve this issue, teams can adopt a canary release strategy. Canary release is a practice in which new software is first released and tested among a small subgroup of users. It’s a good way to “limit the blast radius of a change that goes wrong,” 
