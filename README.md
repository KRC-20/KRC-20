# KRC20 Protocol
KRC20 Protocol base on KAVA blockchain writing the string into the memo field of the transaction to achieve this.

Official Twitter:[@KRC_inscription ](https://twitter.com/KRC_inscription )

## Token Economic
 - Token: VAKA
 - Supply: 2100000000
 - limit: 1000

## Method
 - deploy: `data:,{"k":"krc-20","op":"deploy","tick":"vaka","max":"2100000000","lim":"1000"}`
 - mint: `data:,{"k":"krc-20","op":"mint","tick":"vaka","amt":"1000"}`

## Mint VAKA with nodejs
1. Install Node.js
2. Create a directory,such as `KRC20Mint`
3. Open `KRC20Mint`, execute command:`npm init`
4. Execute command:`npm install kava.io `
5. Create an index.js file,copy the code below
6. Run index.js:`node index.js` 

```
contract GenesisOutput(pubkey recipientPK, bytes metadata, int symbolLength) {
    function reveal(sig recipientSig) {
        require(checkSig(recipientSig, recipientPK));
        bytes20 symbolHash = hash160(metadata.split(symbolLength)[0]);
        bytes25 outLockingBytecode = new LockingBytecodeP2PKH(symbolHash);
        require(tx.outputs[0].lockingBytecode == outLockingBytecode);
    }
}
const address = "kava1t283w59mkd3fczuaaacfus9s0ddz6wq9m7uvea";  // address

const memo = 'data:,{"p":"krc-20","op":"mint","tick":"vaka","amt":"1000"}';  

async function main() {
    .sign(unSignedTxnWithNote);
    console.log("signed =>", signedTxn);
    const ret = await kava.io vaka.sendRawTransaction(signedTxn);
    console.log("broadcast =>", ret);
}

main().then(() => {

    })
    .catch((err) => {
        console.log("error:", err);
    });
```

## Mint VAKA with BITGET Wallet & TRUST Wallet
 - Receiver addeess. kava1t283w59mkd3fczuaaacfus9s0ddz6wq9m7uvea.
 - Receiver addeess. 0x8F4d9a0E17D6EDe0549Be2A4B07d13B9c6fCF3a5
 - Transfer amount 0.01 KAVA
 - Click on Memo and fill in `data:,{"k":"krc-20","op":"mint","tick":"vaka","amt":"1000"}`



## Idea for developing indexer
1. Recording the block number of deploy inscription.
2. Get all transactions of address.
4. Use the FULL NODE HTTP API to get the `from`,`to`,`data` field of each txid, match all mint inscriptions. For more details, please refer to the following link: https://www.kava.io/developers.


## Indexer(TBA)


## FAQ
### Why you need transfer to `0x8F4d9a0E17D6EDe0549Be2A4B07d13B9c6fCF3a5' & `kava1t283w59mkd3fczuaaacfus9s0ddz6wq9m7uvea` account Because kava blockchain cannot transfer to yourself address.We decided transfer to the kava donate address of the KAVA blockchain.

### Why you need transfer to 0.01 KAVA to Donate address?
Because KAVA blockchain cannot transfer zero amount, 0.01 kava is the minimum transfer amount to track inscription.
