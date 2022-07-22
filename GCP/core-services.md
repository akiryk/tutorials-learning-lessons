# Essential Google Cloud Infrastructure: Core Services
June 19, 2022 version

[Source Table of Contents](https://app.pluralsight.com/library/courses/essential-google-cloud-infrastructure-core-services-9/table-of-contents)
[Course Resources](https://s2.pluralsight.com/links/00700a05-c90e-4311-af2c-0a5969905099_8753cf4cc46dd73db26d954eaffcb2ca.pdf)

## Identity and Access Management (IAM)
GCP IAM is composed of several objects
- Organization (e.g. Wayfair)
- Folders (e.g. departments, such as Storefront or Admin, as well as teams within depts)
- Projects
- Resources
- Roles
- Members

**Organization** is the root node. There are two super-users with somewhat different roles, and these are usually two different people.
- Workspace admin: responsibilities include assigning an organization admin (below) and managing lifecycle of the organization resource.
- Organization admin: responsibilities include defining IAM policies, structure of resource hierarchy, and delegating billing responsibilities.

Roles:
- Admin: full control over all resources
- Viewer: can view all resources

**Folders**. These are things like departments or teams within departments, since folders can contain other folders. Folders enable delagation of administration rights. Each head of a deptartment can have full ownership of all of their resources. 

Roles:
- Admin
- Creator
- Viewer

**Projects**.

Roles:
- Creator: if you create, you are the owner of that project
- Deleter

**Roles**

Roles define "can do what, on which resource". There are three types:
- Basic, which are for fixed, coarse-grained level of access. They include Owner, Editor, Viewer, and Billing Admin roles. 
- Predefined: These group permissions together so that users can carry out operations, e.g. to manage an instance of Compute Engine. Different resources have their own [predefined roles](https://cloud.google.com/iam/docs/understanding-roles#predefined). 
- Custom roles enable greater precision in exactly what permissions you grant. E.g. you may want a particular group of users to be able to start and stop an instance of Compute Engine but not modify it or anything else.

Create custom roles by going to GCP > IAM > Roles.

**Members**
This is the who part of roles, "who can do what on which resource". There are five types of members. You can't use IAM to create/manage users and groups; instead, use cloud identity or Workspace to do so. A _policy_ is a list of bindings; a binding is a way to connect members to a role.

Principle of least privilege. This is very important because privileges are inherited from top down. This means that if a user is granted editor privileges at the organization level, they'll also have those privileges at the Folder or Project level _even if_ the Folder or Project is more restrictive.

**Service Account** belongs to an application instead of an end-user; used for server-to-server interactions. 
      
Be cautious when granting the ServiceAccountUser Role to a user or group. 

**Groups** It's generally recommended to grant roles to groups rather than individuals since it's easy to update the group with new members. 

**Best Practices**

- leverage and understand the resource hierarchy (e.g. a project inherits privileges from it's containing folder)
- grant roles to groups rather than individuals
- when using service accounts, be careful with the serviceaccountuser role and give it a clear display name and establish key rotation policies.
- use Cloud IAP to have a central auth layer rather than network-level firewalls. 

## Storage and Database Services

## Resource Management

## Resource Monitoring
