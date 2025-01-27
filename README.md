Celo Network Monitor
====================

![pipeline status](https://gitlab.com/polychainlabs/celo-network-monitor/badges/master/pipeline.svg)

Monitor the health of a Celo validator deployment with alerts like:

![Example Alert](example.png)

## Prerequisites
Linux machine with Docker and docker-compose [installed](https://gist.github.com/alchemydc/77b5c93865a53ef5a8b8e858f24f8f9b).

OR

Cloud provider capable of deploying Docker containers (eg Google Cloud Run or Amazon ECS)

OR

Kubernetes cluster of your choice.

## Quick Start

0. Clone this repo: `git clone https://github.com/alchemydc/celo-network-monitor.git`
1. Edit [template-addresses.mainnet.yaml](template-addresses.mainnet.yaml) to include addresses for your *your* validator group (and any other accounts you wish to monitor)
2. Edit [mainnet.env](mainnet.env) to include *your* Discord webhook
3. `cd docker && docker-compose up`
4. Profit


## Development

First, set the addresses you'd like to monitor in `addresses.<network>.yaml` and set your node and alerting envars in `<network>.env`. 

Then, develop this project locally with:

```shell
# Setup
yarn
# Test
yarn test
# Run locally
ENV_FILE=<network>.env yarn dev
```

## Monitors

Monitors can be enabled or disabled by commenting out desired monitors in `src/monitor/monitor.ts`. Default monitors include:

* **Attestation Service** - Monitor a validator's Attestation service (disabled by default)
* **Balance** - Monitor the CELO and cUSD balances of all addresses specified in the addresses yaml file
* **Electability Threshold** - Monitor the threshold of votes needed to get elected
* **Governance** - Monitor the network for governance activity
* **Key Rotation** - When validator keys are rotated, ensure that they are fully rotated
* **Network Participation** - Monitor overall network participation numbers
* **Node** - Monitor Celo node & network health
* **Pending Votes** - Monitor our addresses for pending votes. Remind us to activate them
* **Validator** - Monitor the health of our validators

## Deployment

The included [build script](docker/docker_build_monitor.sh) and [Dockerfile](docker/Dockerfile) make it easy to package up your changes into a new image and quickly deploy a new container.
