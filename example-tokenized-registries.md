##Tokenized Registries
The Tokenized protocol has a full set of registry actions that are able to support a wide range of registry activities such as Whitelisting, Blacklisting, KYC provisions and more. Registries do not need to be operated by Tokenized Smart Contracts.

A registry is a separate entity to a smart contract, allowing a single registry to be used as an approval gateway for multiple Smart Contracts, or allowing individual smart contracts to have multiple possible approval registries.

Registries provide a way for a smart contract to implement KYC without having to directly manage customer information. When a smart contract is managing an asset for which KYC provisions are in place, a set of approved registries is included in the Asset Creation action. When a customer wishes to transfer this asset, they must provide a signed message from the registry which includes their address, the contract address, the asset code, the receiver's address and any other details required for the transfer to be authorised. The registry takes these details and builds a signature which includes a recent block hash from the blockchain. Registry signatures expires 1 hour after the second block after the one in the signature is found. 

If an Issuer wants to create assets that require receivers to be registered for KYC verification, the asset must be linked to the registry upon creation.

There are four actions involved in the creation and management of a registry.
1. Establishment
2. Addition
3. Alteration
4. Removal

###1. Establishment
The Establishment action shows the Tokenized Smart Contract where a Registry has been created. When a Tokenized Smart Contract is told to look for a registry, it expects to see an Establishment transaction as the first action occurring at that addresss.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/establishment-action.svg?sanitize=true" alt="Establishment action" align="middle">

###2. Addition
The addition action adds an address, handle, username or other to the registry. The entry is added as a message inside the Action payload.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/addition-action.svg?sanitize=true" alt="Addition action" align="middle">

###3. Alteration
The alteration action allows the registry to change the details of a registered entity. The alteration is sent as a message inside the action payload.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/alteration-action.svg?sanitize=true" alt="Alteration action" align="middle">

###4. Removal
The removal action removes the listed entity from the registry. The removal is sent as a message inside the action payload.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/removal-action.svg?sanitize=true" alt="Removal action" align="middle">