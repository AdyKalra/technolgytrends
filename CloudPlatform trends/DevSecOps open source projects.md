[devsecops](https://enterprisersproject.com/article/2021/8/5-devsecops-open-source-projects-know)

### 5 DevSecOps open source projects
Teams that embrace the DevSecOps approach make security an integral part of the entire application life cycle. These open source projects aim to help

1. [Clair](https://github.com/quay/clair)
Vulnerability scanning should be considered table stakes as part of a DevSecOps automated CI/CD workflow. This scanning can take place in multiple places across the workflow – and scanning should continue once software is deployed into production as new threats defined on the Common Vulnerabilities and Exposures database (CVE) are discovered and as changes can occur in deployed images.

Clair is an open source project for the static analysis of vulnerabilities in application containers. Clair is an API-driven analysis engine that inspects containers layer-by-layer for known security flaws. Using Clair, you can build services that provide continuous monitoring for container vulnerabilities.

This type of service is particularly important when organizations download container images directly. However, even when building containers from source, vulnerabilities can creep in over time as new security exploits are discovered.

2. [Sigstore](https://www.sigstore.dev/)
The goal is to provide a free and transparent chain of custody tracing service.
Properly securing a software supply chain involves more than simply doing a point-in-time scan as part of a DevSecOps CI/CD pipeline. With the help of a working partnership that includes Google, the Linux Foundation, Red Hat, and Purdue University, sigstore brings together a set of tools developers, software maintainers, package managers, and security experts can benefit from. It handles the digital signing, verification, and logs data for transparent auditing, making it safer to distribute and use any signed software. The goal is to provide a free and transparent chain of custody tracing service for everyone. This sigstore service will run as a non-profit, public good service to provide software signing.

Cosign, which released its 1.0 version in July 2021, signs and verifies artifacts stored in Open Container Initiative (OCI) registries. It also includes underlying specifications for storing and discovering signatures.

Fulcio is a Root Certificate Authority (CA) for code-signing certificates. It issues certificates based on an Open ID Connect (OIDC) email address.The certificates that Fulcio issues to clients in order for them to sign an artifact are short-lived. As a result, users can sign things and not have to worry about protecting a private key (or trying to revoke one if it’s compromised).

Rekor provides an immutable, tamper-resistant transparent ledger and timestamping service and generates metadata within a software supply chain. Software maintainers and build systems can record signed metadata to an immutable record. Other parties can then query said metadata to let them make informed decisions on trust and non-repudiation of an object’s life cycle.

3. [KubeLinter](https://github.com/stackrox/kube-linter)
KubeLinter builds on the basic vulnerability scanning concept. Traditional vulnerability scanning can be thought of as essentially a unit test. Containers, libraries, and so forth get tested in isolation. Like unit tests, this is a valuable practice in and of itself but there are additional benefits to scanning more complex integrated objects.

KubeLinter checks configurations against a variety of best practices, with a focus on production readiness and security.
KubeLinter checks configurations against a variety of best practices, with a focus on production readiness and security. KubeLinter runs sensible default checks, designed to provide useful information about Kubernetes YAML files and Helm charts. This helps teams check for security misconfigurations and DevSecOps best practices. Some common examples include running containers as a non-root user, enforcing least privilege, and storing sensitive information only in secrets.

Thus, KubeLinter goes beyond scanning for vulnerabilities in a container or library to looking for vulnerabilities in how that software is being configured and used.

4. [Open Policy Agent and Gatekeeper](https://github.com/open-policy-agent/gatekeeper)
One area of Kubernetes security that’s garnered a great deal of interest over the past couple of years is policy management. Open Policy Agent (OPA) has a policy language, Rego, that abstracts away layers of the infrastructure stack and APIs. The bottom line is that OPA simplifies security policy, which is a good thing given that complexity is a common cause of security vulnerabilities.

OPA Gatekeeper is the Kubernetes-native way to integrate OPA into Kubernetes. It uses the OPA Constraint Framework, built with Kubernetes Custom Resource Definitions (CRDs), to describe and enforce policies. With its 3.0 version, Gatekeeper integrates with the OPA Constraint Framework to enforce Kubernetes CRD-based policies and allows declaratively configured policies to be reliably shareable.

This enables the creation of policy templates for Rego policies, creation of policies as CRDs, and storage of audit results on policy CRDs. This project is a collaboration between Google, Microsoft, Red Hat, and Styra.

Subprojects include Rego Playground for Policy Sharing, VS Code for Policy Authoring, and, for ultimate control, CLI and REPL.

5. [Falco](https://falco.org/)
Originally created by Sysdig in 2016, Falco is a run-time threat detection engine for Kubernetes. Falco ships with a default set of rules that check the kernel for unexpected behavior. For example, an alert might be triggered in response to namespace changes, privilege escalations, or unexpected network connections.

Kubernetes Audit Events are also now on Falco’s list of supported event sources. That means that, once a Kubernetes cluster is configured with audit log enabled, it can send audit logs as events to Falco. You can write flexible Falco rules to read these events and detect malicious or other notable activity for any type of host/container behavior or activity. These alerts can be integrated into your incident response workflows to decrease your response time and manage everything through your existing processes.

