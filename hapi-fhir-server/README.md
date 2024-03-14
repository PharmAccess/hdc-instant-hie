
# Instant OpenHIE FHIR Server - docker-swarm

This component consists of:
* Hapi Fhir Server- [HAPI FHIR](https://hapifhir.io/)

## Getting Started

> **The below instructions are only to be used for starting up the FHIR Server manually for local testing outside of the usual Instant OpenHIE start instructions.**

Proceed with care. This very manual deployment can get complicated.
For the regular start up, please see the [README.md](../README.md).

### Prerequisites

* Ensure that docker is installed. For details on how to install docker click [here](https://linuxize.com/post/how-to-install-and-use-docker-compose-on-ubuntu-18-04/).
* have yq installed. You can install it by running the following command
    ```bash
    sudo snap install yq
    sudo apt-get install jq
    ```
* have postgres instance running and update credentials
* install `direnv` by running the following command
    ```bash
    sudo apt install direnv
    ```
* add the following line to your ~/.bashrc file
    ```bash
    eval "$(direnv hook bash)"
    ```
* allow the use of the `.envrc` file by running the following command
    ```bash
    source ~/.bashrc
    direnv allow
    ```

### Start Up Hapi Fhir Services

From the  root directory, run the following command to start up the Hapi FHIR.

```bash
./hapi-fhir-server/swarm.sh init
```

To take down the service run:

```bash
./hapi-fhir-server/swarm.sh destroy
```

To shut down the services run:

```bash
./hapi-fhir-server/swarm.sh down
```

To start the services when they have been stopped run:

```bash
./hapi-fhir-server/swarm.sh up
```

To run in dev mode in which the ports are exposed pass the flag `dev` as done below

```bash
./hapi-fhir-server/swarm.sh init dev
```

## Accessing the services

### HAPI FHIR

This service is accessible for testing.

<http://{BROAD_CAST_IP}:3447>

In a publicly accessible deployment this port should not be exposed. The OpenHIM should be used to access HAPI-FHIR.

## Testing the Hapi Fhir Component

For testing this Component we will be making use of `curl` for sending our request, but any client could be used to achieve the same result.

Execute the command below

```bash
curl http://{BROAD_CAST_IP}:3447/fhir/Patient
```

## Backups

> This section assumes postgres backups are made using `pg_basebackup`

### Postgres (Hapi-FHIR)

To start up Hapi FHIR and ensure that the backups can be made, ensure that you have created the Hapi FHIR bind mount directory (eg./backup)