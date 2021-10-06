# Simple Consent Management

1. Once IS is running login to the console app [localhost:9443/console](https://localhost:9443/console) using `admin:admin` user:pass

1. Create two `New Application` using the `Single Page Application` template

    - __Name__ `JS` app with __Redirect URL__
      ```
      https://localhost:5000/
      ```

    - __Name__ `TS` app with __Redirect URL__
      ```
      http://localhost:3000
      ```

1. Configure different consents for each app `Select App` -> `Attributes` -> select attributes as required and optional for consent

1. Update __Self Registration__ by selecting the `Manage` tab -> `User Onboarding` section

    - set `User self registration` to *Enabled*
    - set `Prompt reCaptcha` to *Disabled*
    - submit changes

1. Follow these [instructions](../README.md#react-apps) to update the web apps with the correct configuration and `clientId`.

1. In a new browser session navigate to the [JS app](https://localhost:5000/) and click the `Login` button

1. Register a new user

1. Open the [local mailserver](http://localhost:8025/) 

1. Activate the new user by clicking the activation like in the registration email.

1. If you are not redirected, navigate back to the [JS app](https://localhost:5000/) and `Login` with the newly created user

1. Select the consents to approve

1. Navigate to to the [TS app](http://localhost:3000) and `Login`. The new user is already logged in

1. Select the new consents to approve

1. Navigate to to the [User Account](http://localhost:9443/myaccount)

1. User can download all PII from `Profile Info` -> `Export Profile`

1. Open the `Security` tab -> show `Manage consents` section

1. Apps consents can be updated and revoked. Revoking mandatory consents will prompt a new request the next time the user logs in.

## Other resources

https://is.docs.wso2.com/en/latest/learn/consent-management/
