# Registration Event Listener

This is a custom event listener for Keycloak events. 
Its goal is to notify an admin about new user registrations via email.

## How to build the artifact?

```sh
mvn clean install
```

## How to build the artifact with docker?

```sh
docker run --rm -v "$PWD":/usr/src/app -w /usr/src/app maven:3-openjdk-11 mvn clean install
```

## How to add the jar in Keycloak?

Copy the jar in the target folder to the `/opt/keycloak/providers/` folder.

Or when using Docker mount the file `./custom-event-listener.jar:/opt/keycloak/providers/custom-event-listener.jar`

## How to configure the event listener in Keycloak?

Set the event listener

1. Open up Keycloak administration console and select your realm
2. Go to **Realm Settings**
3. Go to the **Events** tab
4. Click in the input box next to event listeners and a dropdown with all available event listeners will be shown. Select our newly created `custom_event_listener`


## How to test it?

After you have set up everything and configured the listener do the following:

1. Open the web interface of Mailhog at http://localhost:8085
2. Register a new user on keycloak
3. Go to Mailhog and check that it catched a mail for the admin
