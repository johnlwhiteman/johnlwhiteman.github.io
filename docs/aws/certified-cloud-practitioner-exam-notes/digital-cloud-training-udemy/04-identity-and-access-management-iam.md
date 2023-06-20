# Identity and Access Management (IAM)

## Overview

* A principal is a person or applicaiton that can make a request for an action or operation on an AWS resource
* IAM principals must be authenticated to send requests (few execptions)
* Policy types
    * Identity-based policy
    * Resource-based policy
* Accessible
    * Console
    * CLI
    * API
* Entities
    * User
    * Role
    * Federated User
    * Application
* Methods of Authentication
    * Person -> User name, password, MFA token (optional)
    * CLI/API -> Access Key ID and Secret Access Key

## IAM Users, Groups, Roles, and Policies

***All permissions are implicitly denied by default***

* Users
    * Up to 5000 user accounts can be created
    * Email you used to create/log into account is root - full permissions (bad idea)
    * Users have a friendly name - John
    * Users also have an Amazon Resource Name (ARN) - arn:aws:iam::<some number>:user/John
    * User name/password -> console
    * Access keys -> API/CLI
    * Users have NO permissions by default
* Group
    * Organizes users into groups, e.g., admin, development, hr, ...
    * User gains the permissions applied to the group through a policy
* Roles
    * Used for delgation and are assumed
    * An IAM identity that has specific permissions
    * Roles are assumed by users, applications, and srevices
    * Use roles to delegate policy
* Policies
    * Define the permissions for the identities or resources they are associated with
    * Identity-policies can be applied to users, groups, and roles
    * Policies are documents that define permissions and are written in JSON
* Root User
    * User that created the account
    * Full blown permissions and cannot be restricted

## IAM Authentication and MFA

* John -> UserName/Password/MFA Token -> AWS Management Console
* John -> CLI/API -> Access Key ID/Secret Access Key -> AWS API
    * Used for programmatic access
* MFA
    * Something you know
    * Something you have
        * Virtual/Hardware Device
    * Something you are (not on AWS)

## Service Control Policies (SCPs)

* Feature of AWS organizations
    * Control the maximum available permissions
    * SCPs DON'T grant any permissions, they control the available permissions
* Management account is the root
    * Dev
    * Test
    * ...

## IAM Best Practices

* Require human users to use federation with an identity provider to access AWS using "temporary credentials"
* Requre workloads to use "temporary credentials" with IAM roles to access AWS
* Require MFA
* Rotate access keys regularly for use cases that require long-term credentials
* Safeguard your root user credentials and don't use them for everyday tasks
* Apply least-privilege permissions
* Get started with AWS managed policies and move toward least-privilege permissions
* Use IAM Access Analyzer to generate least-privilege policies based on access activity
* Regulary review and removed unused users, roles, permissions, policies, and credentials
* Use conditions in IAM policies to further restrict access
* Verify public and cross-account access to resources with IAM Access Analyzer
* Use IAM Access Analyzer to validate your IAM policies to ensure secure and functional permissions
* Establish permissions guardrails across multiple accounts
* User permission boundaries to delegate permissions management within an account
* Use roles for applications that run on Amazon EC2 instances
* Use roles to delegate permissions
* Don't share access keys

## References

* [AWS Identity and Access Management](https://digitalcloud.training/aws-identity-and-access-management/)