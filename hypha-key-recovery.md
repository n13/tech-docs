
# Hypha DAO solves key recovery for end users. 

## Whitepaper

### Abstract
We use delayed key recovery to securely recover any account through the hypha DAO, while also allowing users the ability to opt out and be fully decentralized. 
This solves the following issues with crypto users:
- Keys are lost, and because they are held in self custody, customers lose access and funds on their accounts. 

### How we solve the problem:

#### On Chain: 

Recovery Contract (R)
We provide a smart contract which itself has no keys - meaning, no one can alter this contract once it's deployed. 

The smart contract is the same as our guardians contract, but allows for 
- any number of guardians, even 1
- a flexible delay in recovery, example 30 days

Other features of this contract:
- A user can assign N guardians with M/N signatures to recover their account
- A guardian can initiate a recovery for a user - the user provides the public key, the guardian starts the recovery. 
- A user can cancel a recovery in progress any time using their key - meaning if the user still has their old key they can always cancel. 
- A recovery that has all required signatures to recover can be executed by anyone - after the delay specified in setup
- Active recovery can be queried by username to be recovered

Dao contract: A DAO contract has an action to initiate recovery on behalf of dao.hypha - this action uses self permission to call recovery - it also checks that the recoverer who makes the call on behalf of the user is an admin in the dao where the user is a member of. This was dao.hypha recovery can only be initiated by DAO admins. 

#### In the Hypha Wallet

ACCOUNT SETUP with recovery:
In the wallet, when we set up the account, we give owner permission to R by default. We also set up dao.hypha as a 1/1 recovery account, with a 30 day delay. 

SETTINGS:
In the settings screen users can opt out of recovery, or opt in if they have opted out. 

Opt out: A user can turn off recovery. They are advised to write down their secret words again, warned 3 times, then we make a call to remove them from the recovery contract. 

Cancel: If a recovery is in process, but the user is logged in (has the key), a large warning is shown with the option to cancel the recovery. 

Opt in: If they opt in, they are shown an option to select dao.hypha as recovery, or another account, and the delay (default 30 days). They're not allowed to select a value below 24h for recovery. (30 - 7 - 1 days as initial options). They can also choose multiple accounts and M/N recovery permissions for advanced users. 


RECOVERY

Users can initiate recovery on a new wallet by entering their name, they are then given a public key, and a private key to write down. 

The user then must share the public key with dao.hypha - we can do this manually at first through customer service and set up an API later. 

#### Summary

Our system provides the following functions:
- Secure - through the 30 day delay as well as wallet notifications for logged in users, users can cancel fraudulent recovery. 
- Decentralized - Users can opt out completely
- Fraud proof - Users can cancel recovery
- Safe - Users are automatically enrolled so by default if they don't do anything, they are protected
- Ease of use - No writing down key phrases or passwords or other things that have been proven not to work for a significant percentage of users. 