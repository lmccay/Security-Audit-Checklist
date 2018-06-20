# Security-Audit-Checklist

*Tech Preview Security Audit*

For features that are being merged without full security model coverage,
there need to be a base line of assurances that they do not introduce new
attack vectors in deployments that are from actual releases or even just
built from trunk.

*1. UIs*

  1.1. [ ] Are there new UIs added with this merge?

  1.2. [ ] Are they enabled/accessible by default?

  1.3. [ ] Are they hosted in existing processes or as part of a new
process/server?

  1.4. [ ] If new process/server, is it launched by default?

*2. APIs*

  2.1. [ ] Are there new REST APIs added with this merge?

  2.2. [ ] Are they enabled by default?

  2.3. [ ] Are there RPC based APIs added with this merge?

  2.4. [ ] Are they enabled by default?

*3. Secure Clusters*

  3.1. [ ] Is this feature disabled completely in secure deployments?

  3.2. [ ] If not, is there some justification as to why it should be available?

*4. CVEs*

  4.1. [ ] Have all dependencies introduced by this merge been checked for known
issues?


--------------------------------------------------------------------------------------------------------------------------------------------------


*GA Readiness Security Audit*

At this point, we are merging full or partial security model
implementations.
Let's inventory what is covered by the model at this point and whether
there are future merges required to be full.

*1. UIs*

  1.1. [ ] What sort of validation is being done on any accepted user input?
(pointers to code would be appreciated)

  1.2. [ ] What explicit protections have been built in for (pointers to code
would be appreciated):

    1.2.1. [ ] cross site scripting

    1.2.2. [ ] cross site request forgery

    1.2.3. [ ] click jacking (X-Frame-Options)

  1.3. What sort of authentication is required for access to the UIs?

    1.3.1. [ ] Kerberos

      1.3.1.1. [ ] has TGT renewal been accounted for

      1.3.1.2. [ ] SPNEGO support?

      1.3.1.3. [ ] Delegation token?

    1.3.2. [ ] Proxy User ACL?

  1.4. [ ] What authorization is available for determining who can access what
capabilities of the UIs for either viewing, modifying data and/or related
processes?

  1.5. [ ] Is there any input that will ultimately be persisted in configuration
for executing shell commands or processes?

  1.6. [ ] Do the UIs support the trusted proxy pattern with doas impersonation?

  1.7. [ ] Is there TLS/SSL support?

*2. REST APIs*

  2.1. [ ] Do the REST APIs support the trusted proxy pattern with doas
impersonation capabilities?

  2.2. [ ] What explicit protections have been built in for:

    2.2.1. [ ] cross site scripting (XSS)

    2.2.2. [ ] cross site request forgery (CSRF)

    2.2.3. [ ] XML External Entity (XXE)

  2.3. [ ] What is being used for authentication - Hadoop Auth Module?

  2.4. [ ] Are there separate processes for the HTTP resources (UIs and REST
endpoints) or are they part of existing processes?

  2.5. [ ] Is there TLS/SSL support?

  2.6. [ ] Are there new CLI commands and/or clients for accessing the REST APIs?

  2.7. [ ] What authorization enforcement points are there within the REST APIs?

*3. Encryption*

  3.1. [ ] Is there any support for encryption of persisted data?

  3.2. [ ] If so, is KMS and the hadoop key command used for key management?

  3.3. [ ] KMS interaction with Proxy Users?

*4. Configuration*

  4.1. [ ] Are there any passwords or secrets being added to configuration?

  4.2. [ ] If so, are they accessed via Configuration.getPassword() to allow for
provisioning to credential providers?

  4.3. [ ] Are there any settings that are used to launch docker containers or
shell out command execution, etc?

*5. HA*

  5.1. [ ] Are there provisions for HA?

  5.2. [ ] Are there any single point of failures?

*6. CVEs*

Dependencies need to have been checked for known issues before we merge.
We don't however want to list any CVEs that have been fixed but not
released yet.

  6.1. [ ] All dependencies checked for CVEs?
