## Tokenized Registries
The Tokenized protocol has a full set of registry actions that are able to support a wide range of registry activities such as Whitelisting, Blacklisting, KYC provisions and more. Registries do not need to be operated by smart contracts.

There are four actions involved in the creation and management of a registry.
1. Establishment
2. Addition
3. Alteration
4. Removal

### 1. Establishment
The Establishment action shows the Tokenized smart contract where a Registry has been created. When a Tokenized smart contract is told to look for a registry, it expects to see an Establishment transaction as the first action occurring at that addresss.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/establishment-action.svg?sanitize=true" alt="Establishment action" align="middle">

### 2. Addition
The addition action adds an address, handle, username or other to the registry. The entry is added as a message inside the Action payload.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/addition-action.svg?sanitize=true" alt="Addition action" align="middle">

### 3. Alteration
The alteration action allows the registry to change the details of a registered entity. The alteration is sent as a message inside the action payload.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/alteration-action.svg?sanitize=true" alt="Alteration action" align="middle">

### 4. Removal
The removal action removes the listed entity from the registry. The removal is sent as a message inside the action payload.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/removal-action.svg?sanitize=true" alt="Removal action" align="middle">
