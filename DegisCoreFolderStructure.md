# Degis Core Folder Structure
Indicates root folders. Files are not contained in this structure.

```
.
├── archive/                #archived files
│   ├── naughtyPrice-1.0  
│   └── naughtyPrice-2.0 
├── contracts/              #current contracts
│   ├── ILM
│   ├── ChainlinkMock
│   ├── farming
│   ├── governance
│   ├── income
│   ├── libraries
│   ├── lucky-box
│   ├── mocks
│   ├── naughty-price
│   ├── proxy
│   ├── staking
│   ├── tokens
│   └── utils
├── deploy                  #ts files to deploy
├── deployments/            #json deployment files
│   ├── avax
│   ├── avaxTest
│   ├── fuji
│   └── fujiTest
├── deprecated              #deprecated contracts
├── docs/                   #documentation files
│   ├── hardhat-docgen
│   ├── solidity-docgen
│   └── uml
├── info                    #json maps of deployment addresses
├── script/                 #general scripts
│   ├── deploy
│   ├── farming
│   ├── naughtyPrice
│   ├── policyFlow
│   ├── staking
│   ├── tokens
│   └── verify
├── tasks/                  #contract tasks
│   ├── ILM
│   ├── emergencyPool
│   ├── farming
│   ├── general
│   ├── governance
│   ├── incomeSharing
│   ├── lucky
│   ├── miserableFlight
│   ├── naughtyPrice
│   ├── overall
│   ├── proxy
│   ├── staking
│   └── tokens
├── templates               #handlebars file generation template
└── test/                   #hardhat test files
    ├── EmergencyPool
    ├── Farming
    ├── FlightDelay
    ├── Governance
    ├── Income
    ├── Libraries
    ├── LuckyBox
    ├── Staking
    ├── helper
    ├── naughtyPrice
    └── tokens
```