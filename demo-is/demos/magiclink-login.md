# Magiclink Login

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

1. Follow these [instructions](../README.md#react-apps) to update the web apps with the correct configuration and `clientId`.

1. In a new browser session navigate to the [JS app](https://localhost:5000/) and click the `Login` button

1. Register a new user

1. Open the [local mailserver](http://localhost:8025/)

1. Activate the new user by clicking the activation like in the registration email.

## Docs

[Incubator Repo](https://github.com/wso2-incubator/identity-local-auth-magiclink)
