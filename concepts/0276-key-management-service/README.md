# Aries RFC 0276: Key Management Service 
- Authors: Cam Parra, Mike Lodder
- Status: [PROPOSED](/README.md#proposed)
- Since: 2019-10-30
- Status Note: Still needs some review from community members  
- Supersedes: [Aries RFC 0050](https://github.com/hyperledger/aries-rfcs/tree/master/concepts/0050-wallets)
- Start Date: 2018-10-30
- Tags: feature, protocol

## Summary

![mapyouarehere](./youarehere.png)

This RFC will cover the following: 

- What is a Key Management Service? (Here after I will refer to this as KMS)

## Motivation


Agents that do not design key management as a first class citizen are bound to get their security wrong. Here’s why. There are five areas to consider when agents manage keys: what is their purpose, creation, recovery, revocation, and replication. Private keys used for digital signatures or encryption should not be shared among agents or if sharing is required, shared as little as possible. Keys should be as short lived as possible and have a single purpose. This limits the need to replicate keys to other agents, either for dual functionality or recovery purposes, as well as damage in the event of a compromise.


## Tutorial

![aries-kms-tutorial](./arieskms.png)
***

The following tutorial assumes that when you start aries-kms you choose to use LOX that's been configured with your keyring. We will use Alice to go through the process of unlocking her sqlite instance in which she stores her self sovereign credentials. Keep in mind this is for individual use. This should eventually grow to enterprise level and should be broadened by a future RFC.

Alice loads up Aries-KMS cli (for POC purposes). She is prompted to pick a service to handle her keys. She goes to the default that is set to locks and using KeyChain on her MacBook Pro. Lox is then invoked which securely communicates with the Enclave or keyring on the device. The keyring then prompts the user for their **KeyRing** credentials.

![lox-keyring-prompt](./loxkrprompt.png)

The enclave then is securely unlocked and the key creation process begins for the default storage. Then lox uses the enclave to unlock the default stoage and retrieve the handle for the item that was queried.




## Reference

1. **OS Keystore** : native operating system password vault *i.e. MacOS Keyring, Windows Credential Manager* 
2. [**LOX**](https://github.com/hyperledger/aries-rfcs/tree/master/features/0042-lox): A command line tool for accessing various keychains or secure enclaves
3.  Pornin, T., Why Constant Time Crypto, accessed at https://www.bearssl.org/constanttime.html on 2019-10-01

## Drawbacks

This

## Rationale and alternatives

Here are threats that all KMS services and why we think this is a good implementation that will mitigate these threats. 
*** 
### ***Threats***
- Memory access patterns leakage - Attacker can infer contents and/or importance of data based on how it is accessed and frequency of access. Attacker learns the set of matching records.
- Volume leakage - Attacker learns the number of records/responses.
Search pattern leakage - Attacker can infer the contents and/or importance of data based on search patterns–attacker can easily judge whether any two queries are generated from the same keywords or not.
- Rank leakage - Attacker can infer or learn which data was queried
Side channel leakage - Attacker can access or learn the value of the secret material used to protect data confidentiality and integrity through side channels like memory inspection, RAM scraping, attacks with swap access, and timing attacks[3].
- Microarchitectural attacks - Attacker is able to learn secrets through covert channels that target processors (Spectre/Meltdown)
### ***Adversary***
- Network adversary - observes traffic on network. In addition to snooping and lurking, they can also perform fingerprinting attacks to learn who are the endpoints and correlate them to identical entities.
- Snapshot adversary - breaks into server, snapshots system memory or storage. Sees copy of encrypted data but does not see transcripts related to any queries. Trade off between functionality and security.
- Persistent adversary - corrupts server for a period of time, sees all communication transcripts.
- Honest but curious adversary - System Administrator that can watch accesses to the data

****

These are our derived goals from the threats and adversaries mentioned above.

### Goals
- Privacy - Adversary learns as little as possible about data and queries
- Security - Adversary cannot read/decrypt data or queries
- Anonymity - Adversary does not learn who are the data processors
- Performance - Raise the bar for attackers w/o hurting performance too much


## Prior art


## Unresolved questions

- How can we scale this design to enterprise use?
   
## Implementations

*Implementation Notes* [may need to include a link to test results](README.md#accepted).

Name / Link | Implementation Notes
--- | ---
 | 

