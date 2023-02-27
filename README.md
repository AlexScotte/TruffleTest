# Voting system tests

This repository contains the corrected voting system smart contract [Voting.sol](https://github.com/AlexScotte/TruffleTest/blob/master/contracts/Voting.sol)  and all its associated [units tests](https://github.com/AlexScotte/TruffleTest/blob/master/test/votingTests.js).

## How to use

- Clone the repository
- Install dependencies using "npm install dotenv @truffle/hdwallet-provider @openzeppelin/test-helpers @openzeppelin/contracts"
- Run a second terminal and launch a local blockchain using for example ganache
- Deploy in the local blockchain the contract Voting.sol
- Run tests using "truffle test"

## Test cases


### Deployment
***
* Should store the administrator address
* Should default winning proposal ID be 0

### Voter registration
***

**Voter registration started:**

* Should the first status be RegisteringVoters
* Should revert if the caller is not the administrator
* Should generates an event when adding a voter
* Should revert if adding the same voter
* Should not be able to check the stored voter if the caller is not a voter
* Should be able to get the registered voter stored

### Proposals registration
***

**Before starting proposals registration:**
* Should not be able to do anything except starting the proposal registration
* Should revert when trying to add a proposal if the proposal registration is not started

**Proposal registration started:**
* Should generates an event when changing workflow status to start proposal registration
* Should revert when adding a proposal if the caller is not a voter
* Should add a default proposal after starting registration
* Should revert if the proposal is empty
* Should generates an event when adding a proposal
* Should not be able to get a proposal if not voter
* Should revert if the proposal doesn't exists

**Ending proposal registration:**
* Should not be able to to do anything except ending the proposal registration
* Should not be able to close the proposal registration if caller is not the administrator
* Should generates an event when changing workflow status to close proposal registration


### Voting session
***

**Before starting voting session:**

* Should not be able to do anything except starting the voting session
* Should revert when trying to vote if the voting session is not started
* Should not be able to start the voting session if caller is not the administrator


**Voting session started:**
* Should generates an event when changing workflow status to start the voting session
* Should revert when voting if the caller is not a voter
* Should revert if the proposal doesn't exists
* Should generates an event when voter voted
* Should revert if the voter already voted

**Ending voting session:**

* Should not be able to do anything except ending the votes
* Should not be able to end the voting session if caller is not the administrator
* Should generates an event when changing workflow status to end voting session


### Tallying votes
***

**Before starting tally votes**

* Should not be able to do anything except tallying the votes
* Should revert when tallying votes if the voting session is not ended
* Should not be able to tally the votes if caller is not the administrator


**Tallying vote started**

* Should generates an event when changing workflow status to tally votes
* Should returns the correct winning proposal ID

**Ending tally votes**

* Should not be able to do anything, the session is over
