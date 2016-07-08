---
title: Security
---

TODO: intro


## Secure offline accounts (e.g., base and issuing accounts)

One of the simplest methods for securing an account is keeping its secret seed stored on somewhere offline—it could be a computer with no connection to the internet or just a piece of paper in someone’s wallet. Transactions can be created and signed on an offline computer, then saved to a USB drive (or some other means of storage) and transferred to a computer with internet access, which sends the transactions to a Horizon server or Stellar Core instance. If storing the seed on paper instead of a computer, use a program that doesn’t save the seed to create and sign the transaction.

Since an offline computer has no connection, it is extremely hard for someone without physical access to it to access the account’s keys. However, this also makes every transaction an extremely manual process. A common practice instead is to maintain two accounts: one offline account that securely holds the majority of your assets and another online account that holds only a few assets. Most transactions can be performed with the online account and, when its funds are low, a person can manually replenish it from the offline account.

You can think of this method like having both a bank vault and a cash register drawer. Most of the time the vault is closed and locked. It is only opened occasionally (and under specific procedures) to replenish a register drawer that is running low or to store excess funds from a register drawer that is overflowing. If someone attempts to rob the bank, it is extremely hard for them to get away with anything more than what was in the register drawer.


## Require multiple authorizations or signers

Sensitive accounts can be secured by requiring authorization from multiple individuals to make a transaction. Read the [multisignature guide](concepts/multi-sig.md) to learn more about how.

If you require multiple signers, you should also ensure that you do not require all the possible signers to sign a transaction. If one of the signers loses the keys to their account, you will no longer be able to perform transactions if they have to sign them.


## Ensure assets are revocable

If you issue your own assets, you should usually ensure that they can be revoked using the [“authorization revocable” flag on the account](concepts/accounts.md#flags). This allows you to effectively freeze your assets in someone else’s account in case of theft or in other extenuating circumstances.


## What if an account’s keys are compromised?

Because Stellar’s security is based around public key encryption, it’s critical that an account’s secret seed is not shared. Anyone who has access to the seed effectively has control of the account. However, if someone learns your account’s seed or you accidentally share it with someone who shouldn’t know it, you can remove its ability to control the account with the following steps:

1. Make a new account.
2. Add the new account as a signer on the compromised account. (Use the [`set options` operation](concepts/list-of-operations.md#set-options).
3. Remove the compromised key’s signing authority on the compromised account.
4. Now the new account controls the compromised account and the compromised account’s keys are no longer able to sign transactions.

(NOTE: You must notify the owners of other accounts that the compromised account has signing authority or that the keys are compromised. They need to remove the compromised account as a signer as well [and add the new account].)


## What if there’s a bug in Stellar’s code?

Every node keeps a history archive, so you always have a strong and reliable record of what happened. Parties affected by a bug can examine all the historical details and agree on a method of remediation while the bug is being fixed.


## Securing a Stellar Core Instance

It’s generally a good idea to make sure access to Stellar Core is extremely limited. Some ports and paths must be kept open to communicate with other Stellar Core instances, but otherwise, only a Horizon server should have access to most of Stellar Core. Access to Stellar Core’s databases should also be highly restricted (Note: are certain parts of storage write-only and therefore safe to have more permissive access? Need more details and granularity about databases here?).

TODO: best practices here? Are there particular ports that generally should be closed/opened? Is it a good practice to run a configurable HTTP server (e.g. nginx) in front of Core to help control and configure access? What else?

Other general best practices for server security: don’t use standard ports for things like SSH, only open the ports you really need.


## Keep Up to Date with Security Patches

Signing of releases from Stellar.org?
Any kind of feed for releases?
Watch the forums?
????


## For Individuals

TODO: Use a wallet? Encrypt your secret seed with a password? What else?