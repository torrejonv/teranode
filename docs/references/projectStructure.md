# Teranode Project Structure

The Teranode project is structured as follows:

```text
teranode/
│
├── main.go                       # Entry point to start the services
├── main_test.go                  # Top-level integration tests
│
├── Makefile                      # Build, test, and development task automation
│
├── go.mod                        # Go module definition and dependencies
├── go.sum                        # Go module checksums for dependency verification
│
├── settings.conf                 # Global settings with sensible defaults for all environments
├── settings_local.conf           # Developer-specific and deployment-specific settings. Overrides settings.conf. Not tracked in source control.
│
├── README.md                     # Project overview and getting started guide
├── CLAUDE.md                     # AI assistant (Claude Code) instructions for the project
├── LICENSE                       # Project license
├── CODE_OF_CONDUCT.md            # Community code of conduct
├── CONTRIBUTING.md               # Contribution guidelines
├── GOVERNANCE.md                 # Project governance structure
├── RESPONSIBILITIES.md           # Team roles and responsibilities
│
├── Dockerfile                    # Main Dockerfile for containerization
├── .markdownlint.yml             # Markdown linting rules configuration
├── mkdocs.yml                    # MkDocs documentation site configuration
├── sonar-project.properties      # SonarQube code quality analysis configuration
├── staticcheck.conf              # Go static analysis tool configuration
│
├── cmd/                          # Command-line tools, utilities, and library packages
│   ├── aerospikereader/          # Tool for reading data from Aerospike database
│   ├── bitcointoutxoset/         # Utility to convert Bitcoin blockchain data to UTXO set
│   ├── checkblock/               # Package for validating blocks already added to the blockchain
│   ├── checkblocktemplate/       # Tool to validate block templates before mining
│   ├── filereader/               # Utility for reading blockchain data files
│   ├── getfsmstate/              # Tool to retrieve current Finite State Machine state
│   ├── keygen/                   # Cryptographic key generation utility
│   ├── keypairgen/               # Public/private key pair generation utility
│   ├── peercli/                  # Peer network command-line interface for P2P operations
│   ├── seeder/                   # DNS seeder for peer discovery
│   ├── setfsmstate/              # Tool to manually set Finite State Machine state
│   ├── settings/                 # Settings management and validation tools
│   ├── teranode/                 # Main Teranode daemon entry point
│   ├── teranodecli/              # Teranode command-line interface for node management
│   ├── utxopersister/            # UTXO persistence and management utility
│   └── utxovalidator/            # Package for UTXO validation operations
│
├── services/                     # Core microservice implementations
│   ├── alert/                    # Network alert broadcasting and handling service
│   ├── asset/                    # HTTP/WebSocket API server for external client access to blockchain data
│   ├── blockassembly/            # Block assembly service for mining operations
│   ├── blockchain/               # Blockchain state management through Finite State Machine (FSM)
│   ├── blockpersister/           # Service for persisting blocks to storage backends
│   ├── blockvalidation/          # Block validation service for consensus rule enforcement
│   ├── legacy/                   # Legacy Bitcoin protocol compatibility services
│   ├── p2p/                      # Peer-to-peer networking protocol implementation
│   ├── propagation/              # Transaction propagation service (gRPC/UDP/HTTP)
│   ├── rpc/                      # Bitcoin-compatible JSON-RPC interface
│   ├── subtreevalidation/        # Merkle subtree validation service for UTXO verification
│   ├── utxopersister/            # UTXO set persistence service
│   └── validator/                # Transaction validation service against consensus rules
│
├── stores/                       # Data storage layer implementations
│   ├── blob/                     # Binary large object storage (transactions, subtrees) - S3/filesystem/HTTP backends
│   ├── blockchain/               # Blockchain data storage (block headers, chain state) - PostgreSQL/SQLite backends
│   ├── cleanup/                  # Storage cleanup and maintenance utilities
│   ├── txmetacache/             # Transaction metadata caching layer for performance optimization
│   └── utxo/                     # UTXO storage implementation - Aerospike/SQL backends
│
├── docs/                         # Project documentation
│   ├── howto/                    # How-to guides and practical tutorials
│   ├── misc/                     # Miscellaneous documentation and notes
│   ├── overrides/                # MkDocs theme overrides and customizations
│   ├── references/               # Technical reference documentation
│   │   ├── img/                  # Images for reference documentation
│   │   ├── open-rpc/             # OpenRPC API specifications
│   │   ├── protobuf_docs/        # Generated Protobuf API documentation
│   │   ├── services/             # Individual service reference documentation
│   │   ├── settings/             # Settings configuration reference files
│   │   ├── stores/               # Storage layer reference documentation
│   │   ├── kafkaMessageFormat.md # Kafka message format specifications
│   │   ├── projectStructure.md  # This file - project structure overview
│   │   └── [other reference docs] # Additional reference materials
│   ├── sharding/                 # Sharding architecture and implementation documentation
│   ├── staging/                  # Draft documentation and work-in-progress content
│   ├── topics/                   # Topic-based documentation and deep dives
│   └── tutorials/                # Step-by-step tutorials and learning guides
│
├── compose/                      # Docker Compose configurations for different deployment scenarios
│
├── daemon/                       # Daemon process management and lifecycle implementation
│
├── deploy/                       # Deployment configurations, scripts, and infrastructure-as-code
│
├── errors/                       # Centralized error handling, definitions, and error types
│
├── interfaces/                   # Go interface definitions for service contracts and abstractions
│
├── model/                        # Core data models, structures, and domain objects
│
├── pkg/                          # Reusable packages and shared libraries
│
├── scripts/                      # Utility scripts for development, testing, and automation
│
├── settings/                     # Settings management implementation and configuration parsing
│
├── test/                         # Test utilities, integration tests, and test infrastructure
│
├── ui/                           # User interface components
│   └── dashboard/                # Teranode Dashboard UI (Svelte-based web interface)
│
├── ulogger/                      # Unified logging framework implementation
│
└── util/                         # Common utility functions and helper packages
```
