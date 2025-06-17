
## 🛡 Storage Collision / Upgradability Challenge

In this challenge, you'll explore how improperly managed storage in upgradeable contracts can be exploited to bypass intended permissions.

You're given a proxy setup where:

* The **owner** must opt-in before any upgrade is allowed.
* The **admin** can upgrade the proxy, **but only if** the owner has opted in.

However, there's a subtle vulnerability:
A particular variable that controls this "opt-in" status (`_optIn`) **shares the same storage slot** as part of a mapping in the implementation contract. This is what's known as a **storage collision**.

Using what you know about Solidity’s storage layout and how `delegatecall` affects state, your task is to **find a way to change `_optIn` to `true`**—without the owner explicitly doing it—and use that to **perform an unauthorized upgrade**.

To be specific, the storage slot where _optIn lives actually clashes with the balances mapping on the implementation contract. The address `0x47Adc0faA4f6Eb42b499187317949eD99E77EE85`, this allows admin to change _optIn to true by simply sending some tokens to that account thus allowing the admin to upgrade the contract against the will of the owner - you can easily calculate the storage slot for the balance mapping with: `keccack256(abi.encodePacked(uint256(address), uint256(slot))` where address is the key for the balance mapping and slot is the slot in which the mapping sits on storage.

### 🎯 Your Goal:

Use the behavior of storage collisions to trick the contract into thinking the owner has opted in, allowing you to perform an upgrade as the admin.

---

### 🧠 Concepts to Focus On:

* **Storage layout in Solidity**
* **How mappings are stored in storage**
* **Delegatecall and proxy patterns**
* **Upgradeable contract design patterns**
* **How a specific key in a mapping maps to a storage slot**

If you understand how Solidity calculates mapping keys and how storage slots can accidentally overlap, you'll be well on your way.

---

### 🧩 Remember:

You don’t need to brute force anything. This is a logic bug based on how storage is aligned in the proxy + implementation setup.

### 📚 Recommended Reading:

* [Unstructured Storage (OpenZeppelin)](https://blog.openzeppelin.com/upgradeability-using-unstructured-storage/)
* [The State of Smart Contract Upgrades](https://blog.openzeppelin.com/the-state-of-smart-contract-upgrades/)

## Instructions on how to complete the challenge

Please follow the processes below to carry out the task and submit correctly.

- Create a Private Repository and name it ```2025-06-guild-audit-test```
- DO NOT CLONE OR FORK THIS REPOSITORY!
- In your terminal, add this repo as a submodule.
- Write your test performing this exploit either in foundry or hardhat.

If you are only familiar with hardhat, you can add hardhat to foundry or just use your preferred testing tool. Click [Here](https://hardhat.org/hardhat-runner/docs/advanced/hardhat-and-foundry) to do that 

```sh
git submodule add https://github.com/GuildAudits/2025-Cohort-4-Assessment-Test
```

- Make sure your repo is private
- Add DevPelz, josh4324 and Enniwealth as contributors to this repo so we would have access to examine your submission.

GOODLUCK 🧪!!!!

