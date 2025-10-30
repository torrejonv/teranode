# Teranode CLI Documentation

## Overview

The teranode-cli is a command-line interface tool for interacting with Teranode services. It provides various commands for maintenance, debugging, and operational tasks.

## Basic Usage

To access the CLI in a Docker container:

```bash
docker exec -it blockchain teranode-cli


Usage: teranode-cli <command> [options]

    Available Commands:
    aerospikereader      Aerospike Reader
    bitcointoutxoset     Bitcoin to Utxoset
    checkblock           Check block - fetches a block and validates it using the block validation service
    checkblocktemplate   Check block template
    export-blocks        Export blockchain to CSV
    filereader           File Reader
    fix-chainwork        Fix incorrect chainwork values in blockchain database
    getfsmstate          Get the current FSM State
    import-blocks        Import blockchain from CSV
    resetblockassembly   Reset block assembly state
    seeder               Seeder
    setfsmstate          Set the FSM State
    settings             Settings
    utxopersister        Utxo Persister
    validate-utxo-set    Validate UTXO set file

    Use 'teranode-cli <command> --help' for more information about a command

```

## Available Commands

### Configuration

| Command     | Description                  | Key Options |
|-------------|------------------------------|-------------|
| `settings`  | View system configuration    | None        |

### Data Management

| Command            | Description                          | Key Options                                   |
|--------------------|--------------------------------------|-----------------------------------------------|
| `aerospikereader`  | Read transaction data from Aerospike | `<txid>` - Transaction ID to lookup           |
| `bitcointoutxoset` | Convert Bitcoin data to UTXO set     | `--bitcoinDir` - Location of bitcoin data     |
|                    |                                      | `--outputDir` - Output directory for UTXO set |
|                    |                                      | `--skipHeaders` - Skip processing headers     |
|                    |                                      | `--skipUTXOs` - Skip processing UTXOs         |
|                    |                                      | `--blockHash` - Block hash to start from      |
|                    |                                      | `--previousBlockHash` - Previous block hash    |
|                    |                                      | `--blockHeight` - Block height to start from  |
|                    |                                      | `--dumpRecords` - Dump records from index     |
| `export-blocks`    | Export blockchain data to CSV        | `--file` - CSV file path to export            |
| `import-blocks`    | Import blockchain data from CSV      | `--file` - CSV file path to import            |
| `utxopersister`    | Manage UTXO persistence              | None                                          |

### System Tools

| Command              | Description                   | Key Options                                                      |
|----------------------|-------------------------------|------------------------------------------------------------------|
| `checkblock`         | Validate an existing block    | `<blockhash>` - Hash of the block to validate                    |
| `checkblocktemplate` | Check block template validity | None                                                             |
| `seeder`             | Seed initial blockchain data  | `--inputDir` - Input directory for data                          |
|                      |                               | `--hash` - Hash of the data to process                           |
|                      |                               | `--skipHeaders` - Skip processing headers                        |
|                      |                               | `--skipUTXOs` - Skip processing UTXOs                            |
| `filereader`         | Read and process files        | `--verbose` - Enable verbose output                              |
|                      |                               | `--checkHeights` - Check heights in UTXO headers                 |
|                      |                               | `--useStore` - Use store                                         |
| `validate-utxo-set`  | Validate UTXO set file        | `--verbose` - Enable verbose output showing individual UTXOs     |
| `getfsmstate`        | Get the current FSM state     | None                                                             |
| `setfsmstate`        | Set the FSM state             | `--fsmstate` - Target FSM state                                  |
|                      |                               | &nbsp;&nbsp;Values: running, idle, catchingblocks, legacysyncing |
| `resetblockassembly` | Reset block assembly state    | `--full-reset` - Perform full reset including clearing mempool  |

### Database Maintenance

| Command              | Description                                    | Key Options                                                      |
|----------------------|------------------------------------------------|------------------------------------------------------------------|
| `fix-chainwork`      | Fix incorrect chainwork values in blockchain  | `--db-url` - Database URL (required)                            |
|                      | database                                       | `--dry-run` - Preview changes without updating (default: true)   |
|                      |                                                | `--batch-size` - Updates per transaction (default: 1000)        |
|                      |                                                | `--start-height` - Starting block height (default: 650286)      |
|                      |                                                | `--end-height` - Ending block height (default: 0 for tip)       |

## Detailed Command Reference

### Aerospike Reader

```bash
teranode-cli aerospikereader <txid>
```

Retrieves transaction data from an Aerospike database using the provided transaction ID.

### Bitcoin to UTXO Set

```bash
teranode-cli bitcointoutxoset --bitcoinDir=<bitcoin-data-path> --outputDir=<output-dir-path> [options]
```

Options:

- `--bitcoinDir`: Location of Bitcoin data (required)
- `--outputDir`: Output directory for UTXO set (required)
- `--skipHeaders`: Skip processing headers
- `--skipUTXOs`: Skip processing UTXOs
- `--blockHash`: Block hash to start from
- `--previousBlockHash`: Previous block hash
- `--blockHeight`: Block height to start from
- `--dumpRecords`: Dump records from index

### Check Block

```bash
teranode-cli checkblock <blockhash>
```

Validates an existing block by its hash. This command performs comprehensive validation including:

- Transaction validation
- Merkle tree verification
- Proof of work validation
- Consensus rule checks

**Example:**

```bash
teranode-cli checkblock 000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f
```

### File Reader

```bash
teranode-cli filereader [path] [options]
```

Options:

- `--verbose`: Enable verbose output
- `--checkHeights`: Check heights in UTXO headers
- `--useStore`: Use store

### FSM State Management

```bash
teranode-cli getfsmstate
```

Gets the current FSM state of the system.

```bash
teranode-cli setfsmstate --fsmstate=<state>
```

Options:

- `--fsmstate`: Target FSM state (required)
    - Valid values: running, idle, catchingblocks, legacysyncing

### Export Blocks

```bash
teranode-cli export-blocks --file=<path>
```

Exports blockchain data to a CSV file.

Options:

- `--file`: CSV file path to export (required)

### Import Blocks

```bash
teranode-cli import-blocks --file=<path>
```

Import blockchain data from a CSV file.

Options:

- `--file`: CSV file path to import (required)

### Check Block Template

```bash
teranode-cli checkblocktemplate
```

Validates the current block template. Useful for miners to ensure block templates are correctly formed.

### Seeder

```bash
teranode-cli seeder --inputDir=<input-dir> --hash=<hash> [options]
```

Options:

- `--inputDir`: Input directory for UTXO set and headers (required)
- `--hash`: Hash of the UTXO set / headers to process (required)
- `--skipHeaders`: Skip processing headers
- `--skipUTXOs`: Skip processing UTXOs

### Reset Block Assembly

```bash
teranode-cli resetblockassembly [--full-reset]
```

Resets the block assembly state. Useful for clearing stuck transactions or resetting mining state.

Options:

- `--full-reset`: Perform a comprehensive reset including clearing mempool and unmined transactions

### Validate UTXO Set

```bash
teranode-cli validate-utxo-set [--verbose] <utxo-set-file-path>
```

Validates a UTXO set file for integrity and correctness. This tool is useful for ensuring UTXO set integrity and detecting any inconsistencies.

Options:

- `--verbose`: Enable verbose output showing individual UTXOs

**Example:**

```bash
teranode-cli validate-utxo-set --verbose /data/utxos/utxo-set.dat
```

### Fix Chainwork

```bash
teranode-cli fix-chainwork --db-url=<database-url> [options]
```

Fixes incorrect chainwork values in the blockchain database. This command is used for database maintenance and should be used with caution.

Options:

- `--db-url`: Database URL (postgres://... or sqlite://...) (required)
- `--dry-run`: Preview changes without updating database (default: true)
- `--batch-size`: Number of updates to batch in a transaction (default: 1000)
- `--start-height`: Starting block height (default: 650286)
- `--end-height`: Ending block height (0 for current tip) (default: 0)

⚠️ **Warning**: This command modifies blockchain database records. Always run with `--dry-run=true` first to preview changes before applying them to production databases.

## Error Handling

The CLI will exit with status code 1 when:

- Invalid commands are provided
- Required arguments are missing
- Command execution fails

## Environment

The CLI is available in all Teranode containers and automatically configured to work with the local Teranode instance.
