# SSO with OAuth demo Node SPA

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

1. navigate to to the [TS app](http://localhost:3000) and `Login`

1. New user is already logged in

1. From the `TS` app click the `Logout` button. IS will prompt to confirm.

1. Open the `JS` app and click the `Logout` button. IS __Does Not__ propmt for confirmation because the user is already logged out.

1. The console output of the running IS should have the audit logs of all of the user activity

    - If you don't see logs you can run `docker-compose logs -f identity-server` again to view them
