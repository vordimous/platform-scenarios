# User Registration Approval

1. Once IS is running login to the console app [localhost:9443/console](https://localhost:9443/console) using `admin:admin` user:pass

1. Create two `New Application` using the `Single Page Application` template

    - __Name__ `JS` app with __Redirect URL__
      ```
      https://localhost:5000/
      ```

1. Update __Self Registration__ by selecting the `Manage` tab -> `User Onboarding` section

    - set `User self registration` to *Enabled*
    - set `Prompt reCaptcha` to *Disabled*
    - submit changes

1. Create an Approver user

1. Create workflow definition

1. Create Workflow engagement

1. Register a new user

1. Open the [local mailserver](http://localhost:8025/)

1. Activate the new user by clicking the activation like in the registration email.

1. Approver approves new user

1. New user can now login to the `JS` app

## Other resources

https://is.docs.wso2.com/en/latest/learn/self-registration/
