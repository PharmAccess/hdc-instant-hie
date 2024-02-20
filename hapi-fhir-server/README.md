
# Instant OpenHIE FHIR Server - docker-swarm

This component consists of:
* Hapi Fhir Server- [HAPI FHIR](https://hapifhir.io/)

## Getting Started

> **The below instructions are only to be used for starting up the FHIR Server manually for local testing outside of the usual Instant OpenHIE start instructions.**

Proceed with care. This very manual deployment can get complicated.
For the regular start up, please see the [README.md](../../README.md).

### Prerequisites

Ensure that docker is installed. For details on how to install docker click [here](https://linuxize.com/post/how-to-install-and-use-docker-compose-on-ubuntu-18-04/).
For installing docker click [here](https://linuxize.com/post/how-to-install-and-use-docker-on-ubuntu-18-04/).

For our compose scripts to work, one needs to be able to run docker commands without the `sudo` preface. You can configure your system to run without needing the `sudo` preface by running the following command

```bash
./configure-docker.sh
```

Ensure that you have postgres instance running.

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

To run in dev mode in which the ports are exposed pass the flag `--dev` as done below

```bash
./hapi-fhir-server/swarm.sh init --dev
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