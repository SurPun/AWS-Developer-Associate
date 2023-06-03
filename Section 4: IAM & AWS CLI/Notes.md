# Section 4: IAM & AWS CLI

12. IAM Users should have least privilege which is a principle of granting only the permissions required to complete a task.

13. IAM Policies (Manged by AWS or Custom created by users.)

- IAM Policies Structure

  Consists of :

      - Version: policy language version, always include ‘201 2-10-7"
      - Id:an identifier for the policy (optional)
      - Statement: one or more individual statements (required)
        Statements consists of
        - Sid: an identifier for the statement (optional)
        - Effect: whether the statement allows or denies access(Allow, Deny)

14. MFA