![highestnumber](https://github.com/user-attachments/assets/6128313d-cced-4431-a290-b18ee25eb920)

# Highest Number A Minigame Hook 

## Introduction

Highest Number is a hook programmed in C for the Xahau blockchain. A hook is a series of rules that enable smart logic in Xahau, considered the smart contracts of Xahau.

Highest Number is a Hook that converts a Xahau account in an engine for a simple game. This a simple idea for others to use to create more sophisticated and customizable hooks.

## Explanation


**Attention:** Only use if you are sure of what you are doing on Testnet/Mainnet. You could put your funds at risk. It is recommended to install on new accounts.

The hook when installed allows you to play the game of the largest number. The hook will accept two players sending 1 XAH. With each payment the hook will check the sequence of the current ledger. The hook will store the rightmost number of the ledger sequence and store it in the namespace next to the address of the first player referring to the first payment he receives. When a second player sends a payment of 1 XAH to the hook address, the hook will check the sequence and compare the rightmost number with that of the first player. This can lead to 3 possible outcomes. Player 1 has the largest number and receives the 2 XAH. Player 2 has the largest number and receives the 2 XAH. There is a tie and each player receives 1 XAH. 

The hook blocks any payment other than 1 XAH. So a fourth case could occur, that the hook account runs out of funds and the game cannot be managed. If there are insufficient funds it might not be possible to send the “prize” to the winners. Therefore, it has been enabled to manage an account known as funding “FUND” that the hook allows to operate payments in both directions to be able to take out or put in XAH and avoid the mentioned problem. To assign a “FUND” account it is necessary to create an Invoke transaction from the Hook account with the parameter “FUND” and the account that we want to assign as a “FUND” account in the parameter value. The process is explained below.

## Installation & Usage

Once the hook is installed, the following triggers are expected for the hook.

- An account will send a payment of 1 XAH to the hook account. The payment account will be known as Player 1. The hook will register in the namespace the address of Player one with the key P1AD and store the rightmost number of the ledger sequence in the namespace under the key P1LG.

- A second account (different from the first one) will send a payment of 1 XAH to the hook account. The payment account will be known as Player 2. The hook will compare the rightmost number of the ledger sequence of the ledger sequence with that of Player 1 and decide the final result of the game.

- An Invoke transaction from the hook account with the hook parameter “FUND” and the desired address as value in HEX format. This will store in the namespace the information with the key “FUND” and with value the address in HEX.


## How to install the Highest Number Hook on Testnet?

HookHash: E31E3F125C377E89ACC76610DD017FBEE434FB5BDAE86DEF3C345B994916C64F

1. You can do it by (XRPLWin Hook Install Tool)[https://xahau-testnet.xrplwin.com/tools/hook/from-hash]

2. Or you can do it sending the transaction below:

HookOn is activated to trigger for Invoke and Payment transactions. You can verify it copying the HookOn value (FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF7FFFFFFFFFFFFFFFFFFBFFFFE) in this website: https://richardah.github.io/xrpl-hookon-calculator/

    const prepared = {
      "TransactionType": "SetHook",
      "Account": your_account_address,
      "Flags": 0,
      "Hooks": [
        {
          "Hook": {
            "HookHash": "1A9D1EEA98A9BE3C45A35872E51E36B6E73CBB7033A96CE0D98DB484215E0494",
            "HookNamespace": "0000000000000000000000000000000000000000000000000000000000000000",
            "HookOn": "FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF7FFFFFFFFFFFFFFFFFFBFFFFE",
          }
        }
      ],
      ...networkInfo.txValues,
    };

## How to uninstall the Highest Number Hook on Mainnet/Testnet?

    const prepared = {
      "TransactionType": "SetHook",
      "Account": your_account_address,
      "Flags": 0,
      Hooks:
    [        
        {                        
            Hook: {
                CreateCode: "",
                Flags: 1,
            }
        }
    ],
      ...networkInfo.txValues,
    };

## Transaction Examples for Hook Parameters

## Adding the FUND account

We create a Invoke transaction with our Hook Account as "Account" and NO Destination Account. 

Hook Parameters and values will be:
- FUND
- funding_address

In this example we are using 1E2D42546C8A5270D4E182FAE3D12186F2A32A7E that is the translated version of the address rskZVQvBEXAwsBTFsgEZMBfwnhC7oydSnp. You can visit https://transia-rnd.github.io/xrpl-hex-visualizer/ , Insert the account and click on From Hex, you will see the xrpAddress will be the same as we added. FUND string is HEX translated: 46554E44. (For https://builder.xahau.network/ IDE you don't need to translate Parameter Name)

    const prepared = {
      TransactionType: "Invoke",
      Account: your_account_address,
      Flags: 0,
      HookParameters: [
        {
          HookParameter: {
            HookParameterName: "46554E44",
            HookParameterValue: "1E2D42546C8A5270D4E182FAE3D12186F2A32A7E",
          },
        },
        ],
      ...networkInfo.txValues,
    };



## How to install the Highest Number Hook on Mainnet?

Same as Testnet but changing the hookhash. The Hookhash is B5822426DFE897EF446BBCDEC3F83D803EC80188390DDA74112F6AAFE202A9E8.

1. You can do it by [XRPLWin Hook Install Tool](https://xahau.xrplwin.com/tools/hook/from-hash)

2. Or you can do it sending the transaction below:

```
    const prepared = {
      "TransactionType": "SetHook",
      "Account": your_account_address,
      "Flags": 0,
      "Hooks": [
        {
          "Hook": {
            "HookHash": "B5822426DFE897EF446BBCDEC3F83D803EC80188390DDA74112F6AAFE202A9E8",
            "HookNamespace": "0000000000000000000000000000000000000000000000000000000000000000",
            "HookOn": "FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF7FFFFFFFFFFFFFFFFFFBFFFFE",
          }
        }
      ],
      ...networkInfo.txValues,
    };
```

## Ideas for your hooks

This is just a small example so that others can build similar ideas or extend the current hook. Some ideas I propose:

1. Use timestamps and ledger sequences to expire the game if the second player doesn't send a payment after some time.
2. Let several accounts to play.
3. Save players payment and start the game at the beginning of each day.
4. If both numbers are the same, create a new loop to get a winner after a second round of payments.

## Special thanks

Thanks to [@denis_angell](https://x.com/angell_denis) and [@Satish_nl](https://x.com/angell_denis) for being there when i get stuck.
