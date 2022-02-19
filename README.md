# ECO Stake 🌱 Zabbix Templates

These templates are from a Zabbix 5.0.6 installation. Each template is available as a named file in each subdirectory, or all can be imported at once using the [all-templates.xml](https://raw.githubusercontent.com/eco-stake/zabbix-templates/master/all-templates.xml) file.

Each template is outlined below with the relevant items, triggers and graphs. Configuration is via Macros.

You will likely want to adjust various thresholds and choose which alert types to send a notification for.

## Tendermint Node

This template provides the base attributes, config and triggers of a Tendermint node, including validators. Data is sourced from the nodes RPC server.

[View XML](https://raw.githubusercontent.com/eco-stake/zabbix-templates/master/tendermint-node/tendermint-node.xml)

### Items

- Node ID
- Latest block height
- Latest block timestamp
- Latest block delay
- Number of Peers
- Catching Up
- Delegations
- Delegations last change (positive change only)

### Triggers

- Block Delay
- Block Delay Warning
- RPC Failure
- Delegation increase
- Delegation decreate

### Graphs

- Latest block delay
- Number of peers
- Delegations
- Delegations change

### Configuration

|Configuration|Default|Description|
|--|--|--|
|{$RPC_URL}| |RPC node to connect to; http://myip:26657|
|{$ALLOWED_DELAY}|25|Block delay allowed before initial alert|
|{$ALLOWED_DELAY_WARN}|120|Block delay allowed before warning alert|
|{$DENOM_FACTOR}|1|Adjust the reported voting power for networks like Nomic|

## Mintscan Validator

Inherits from Tendermint Validator. Provides additional attributes and triggers for a validator sourced from Mintscan.

[View XML](https://raw.githubusercontent.com/eco-stake/zabbix-templates/master/mintscan-validator/mintscan-validator.xml)

### Items

- Missed blocks
- Validator rank
- Jailed

### Triggers

- Block missed
- Block missed warning
- Rank increase
- Rank decrease

### Graphs

- Missed blocks
- Validator rank

### Configuration

|Configuration|Default|Description|
|--|--|--|
|{$NETWORK}| |Network this node belongs to. Match minstscan naming convention, e.g. crypto-org|
|{$VALIDATOR_ADDRESS}| |Validator's valoper address|
|{$BLOCK_MISSED_WARN}|10|Number of blocks before sending a HIGH notification. A notification is already sent after 1 block missed.|
