---
title: Time Capsule Encryption via VDF
description: A method to encrypt content on-chain with a pre-determined time delay for decryption.
author: Hojay (@hojayxyz), Igor (@igorperic17), Branko (@saicoder), Ivan (@IvanLudvig)
discussions-to: n/a
status: Draft
type: Standards Track
category: Core
created: 2023-11-18
requires: n/a
---

## Abstract

This Ethereum Improvement Proposal introduces a 'Time Capsule' mechanism to securely encrypt content on the Ethereum blockchain with a pre-defined time delay for decryption, using Verifiable Delay Functions (VDFs). It allows users to upload encrypted content (text or files) and ensures that decryption occurs only after the specified delay, irrespective of computing power advancements, thereby enhancing Ethereum's data handling capabilities for time-sensitive applications.

## Motivation

The current Ethereum ecosystem lacks a mechanism for time-bound data confidentiality. This EIP proposes a solution to securely encrypt and store content on-chain, which remains inaccessible until a predetermined future time. This functionality is crucial for various applications like sealed bidding, time-locked messages, and secure digital inheritance, enhancing Ethereum's utility in handling time-sensitive information.

## Specification

The 'Time Capsule' encryption mechanism is proposed to enable secure on-chain storage of content (text or files) with a predetermined time delay for decryption, using Verifiable Delay Functions (VDFs). The process is as follows:

1. **Encryption and Time Delay Setting:**
   - Users MUST encrypt their content using a specified encryption algorithm (e.g., AES-256).
   - During encryption, users MUST set a time delay for decryption, specified in blocks or time units (e.g., days, hours).
   - The encrypted content and time delay information MUST be encapsulated in a smart contract deployed on the Ethereum blockchain.

2. **Verifiable Delay Function Integration:**
   - A Verifiable Delay Function (VDF) MUST be employed to ensure that the decryption process adheres to the specified time delay.
   - The VDF MUST be designed so that its execution time is predictable and linearly dependent on the number of operations, and it MUST NOT be susceptible to acceleration through parallel processing.
   - Upon completion of the VDF execution, a decryption key or mechanism SHALL be made available.

3. **Decryption Process:**
   - Once the set time delay has elapsed, as determined by the VDF, nodes on the Ethereum network MAY begin the decryption process.
   - The decryption process MUST ensure that only after the specified time delay has elapsed, the content becomes accessible.
   - A self-validation mechanism MUST be included to verify the integrity and authenticity of the decrypted content.

4. **On-Chain Verification and Interaction:**
   - Smart contracts involved in the 'Time Capsule' mechanism MUST include functions to verify the status of the time delay and to initiate the decryption process post delay.
   - Users and recipients MUST be able to interact with the smart contract to retrieve the status of the encrypted content and access it post the time delay.

5. **Gas and Transaction Fee Management:**
   - The smart contract MUST handle the transaction and gas fees required for deploying the contract, performing the VDF, and executing the decryption process.
   - It MUST specify the fee structure and rewards for nodes participating in the decryption process.

The implementation of the 'Time Capsule' mechanism SHOULD adhere to existing Ethereum standards and practices to ensure compatibility and interoperability with current Ethereum infrastructure.

## Rationale

The use of VDFs ensures a guaranteed time delay for decryption, immune to acceleration by computational power increases. This approach ensures that encrypted content remains secure until the predefined time, addressing the need for reliable time-locked encryption on the blockchain.

## Backwards Compatibility

No backward compatibility issues found.

## Test Cases

The following test cases are designed to validate the core functionalities of the 'Time Capsule' encryption mechanism using Verifiable Delay Functions (VDFs). Implementations of this EIP MUST pass all the following tests:

1. **Encryption and Time Delay Setting Test:**
   - **Objective:** Verify that content can be encrypted and a time delay for decryption can be set correctly.
   - **Procedure:**
     - Encrypt a sample text or file using the specified encryption algorithm.
     - Set a specific time delay for decryption.
     - Store the encrypted content and time delay information in a smart contract.
   - **Expected Result:** The smart contract accurately reflects the encrypted content and the set time delay.

2. **Verifiable Delay Function Execution Test:**
   - **Objective:** Ensure that the VDF adheres to the specified time delay and cannot be expedited.
   - **Procedure:**
     - Initiate the VDF with a predefined number of operations correlating to the set time delay.
     - Attempt to process the VDF using varying computational resources.
   - **Expected Result:** The VDF takes the same amount of time to complete regardless of computational resources, adhering strictly to the set time delay.

3. **Decryption Post Time Delay Test:**
   - **Objective:** Validate that decryption occurs only after the specified time delay.
   - **Procedure:**
     - After the time delay set in the VDF has elapsed, initiate the decryption process.
     - Verify the integrity and authenticity of the decrypted content.
   - **Expected Result:** Decryption is successful and accurate only after the VDF has completed, and the content matches the original pre-encryption data.

4. **Smart Contract Interaction Test:**
   - **Objective:** Confirm that users and recipients can interact with the smart contract as intended.
   - **Procedure:**
     - Query the smart contract for the status of the encrypted content and time delay.
     - After the time delay, access the decrypted content via the smart contract.
   - **Expected Result:** The smart contract responds correctly to queries and allows access to decrypted content post time delay.

5. **Gas and Fee Management Test:**
   - **Objective:** Verify that the smart contract correctly handles fees for contract deployment, VDF execution, and decryption.
   - **Procedure:**
     - Deploy the smart contract and execute the 'Time Capsule' process, noting the transaction and gas fees.
     - Reward nodes participating in the decryption process as specified.
   - **Expected Result:** Fees are correctly calculated, charged, and distributed according to the smart contract's specifications.

Implementers are encouraged to add more test cases to cover edge cases specific to their implementation details and to ensure comprehensive testing of all functionalities.


## Reference Implementation

https://github.com/igorperic17/memento/


## Security Considerations


## Copyright

Copyright 2023
