# Bridging

## Fast withdraw

```shell
curl --location --request POST 'http://app.api.sportx.bet/bridge/fast-exit/lock' \
--header 'Content-Type: application/json' \
--data-raw '{"owner":"0x92B1BE018E7Ef135838dF996F0c0e4cFaafe8c8F","spender":"0xC1b6dA1545D81684D4cf08A999B099f52C828E51","tokenAddress":"0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063","amount":"100000000000000000000","signature":"0xef8c1293c948bf1fd9ecc81003b6190f6e006fd2d746fcd9c9e8d29ce08d364c1884272d183b5792d275fa624408f372df742b15d143ffc90fd8c0fe179763031b"}'
```

```javascript
import { BigNumber, Contract, providers, utils, Wallet } from "ethers";
import { parseUnits } from "ethers/lib/utils";
import fetch from "node-fetch";
import ethSigUtil from "eth-sig-util";

async function fastExit() {
  const privateKey = process.env.PRIVATE_KEY!;
  const tokenAddress = process.env.TOKEN_ADDRESS!;
  const fastExitSpenderAddress = process.env.FAST_EXIT_SPENDER_ADDRESS; // See the request payload for what this should be 
  const bufferPrivateKey = Buffer.from(privateKey!.substring(2), "hex");
  const withdrawAmount = parseUnits("100", 18);
  // Note that because this transaction is executing on polygon, you must pass a JSON-RPC endpoint for Polygon, not Ethereum mainnet.
  const wallet = new Wallet(privateKey).connect(
    new providers.JsonRpcProvider(process.env.POLYGON_PROVIDER_URL)
  );

  const tokenContract = new Contract(
    tokenAddress,
    [
      {
        constant: false,
        inputs: [
          { internalType: "address", name: "usr", type: "address" },
          { internalType: "uint256", name: "wad", type: "uint256" },
        ],
        name: "approve",
        outputs: [{ internalType: "bool", name: "", type: "bool" }],
        payable: false,
        stateMutability: "nonpayable",
        type: "function",
      },
      {
        inputs: [
          {
            internalType: "address",
            name: "user",
            type: "address",
          },
        ],
        name: "getNonce",
        outputs: [
          {
            internalType: "uint256",
            name: "nonce",
            type: "uint256",
          },
        ],
        stateMutability: "view",
        type: "function",
      },
      {
        inputs: [
          {
            internalType: "address",
            name: "owner",
            type: "address",
          },
        ],
        name: "nonces",
        outputs: [
          {
            internalType: "uint256",
            name: "",
            type: "uint256",
          },
        ],
        stateMutability: "view",
        type: "function",
        constant: true,
      },
    ],
    wallet
  );

  let nonce: BigNumber;
  if (
    tokenAddress === "0x2791Bca1f2de4661ED88A30C99A7a9449Aa84174" // USDC has a non-standard get nonce method
  ) {
    nonce = await tokenContract.nonces(wallet.address);
  } else {
    nonce = await tokenContract.getNonce(wallet.address);
  }
  const tokenName: string = await tokenContract.name();
  const abiEncodedFunctionSig = tokenContract.interface.encodeFunctionData(
    "approve",
    [fastExitSpenderAddress, withdrawAmount]
  );

  const approveProxySigningPayload = {
    types: {
      EIP712Domain: [
        { name: "name", type: "string" },
        { name: "version", type: "string" },
        { name: "verifyingContract", type: "address" },
        { name: "salt", type: "bytes32" },
      ],
      MetaTransaction: [
        { name: "nonce", type: "uint256" },
        { name: "from", type: "address" },
        { name: "functionSignature", type: "bytes" },
      ],
    },
    domain: {
      name: tokenName,
      version: "1",
      salt: utils.hexZeroPad(utils.hexlify(137), 32),
      verifyingContract: tokenAddress,
    },
    message: {
      nonce,
      from: wallet.address,
      functionSignature: abiEncodedFunctionSig,
    },
    primaryType: "MetaTransaction",
  };

  // log.info("------- fastExit approveSpenderPayload", inspect(signaturePayload));

  const approveSpenderSignature = ethSigUtil.signTypedData_v4(bufferPrivateKey, {
    data: approveProxySigningPayload,
  });

  const payload = {
    owner: wallet.address,
    spender: fastExitSpenderAddress,
    tokenAddress: tokenAddress,
    amount: withdrawAmount.toString(),
    signature: approveSpenderSignature,
  };

  // log.info("------- fastExit payload", inspect(payload));

  const response = await fetch(
    "https://app.api.sportx.bet/bridge/fast-exit/lock",
    {
      method: "POST",
      body: JSON.stringify(payload),
      headers: { "Content-Type": "application/json" },
    }
  );
}
```

> The above command returns JSON structured like this

```json
{ "status": "success" }


```

This endpoint allows users to bridge assets from Polygon to Ethereum mainnet in an instant and trust-minimized manner. A fee is charged in-kind on the transaction, meaning that you are charged a dollar amount worth of the token you are withdrawing as payment for the decreased transaction time. For example if you withdraw $1000 DAI and the fee is $50, you will receive $950 DAI on Ethereum mainnet. Therefore, this is an effective minimum on the withdraw amount. Please see [the fee section](#fast-withdraw-fees) for what this fee is currently set it. 

Transactions are usually processed within a minute compared to ~45m on the official Polygon bridge, but might be longer if Polygon is significantly clogged.

<aside class="warning">
Attempting to withdraw less than the fee amount will not work and you will receive $0 on Ethereum mainnet. 
</aside>

### HTTP Request

`POST https://app.api.sportx.bet/bridge/fast-exit/lock`

### Request payload parameters

Name | Required | Type | Description
--- | --- | --- | ---
owner | true | string | The account whose tokens you wish to bridge
spender | true | string | The bridge address. Must be `0xC1b6dA1545D81684D4cf08A999B099f52C828E51`
tokenAddress | true | string | The token contract address on polygon that you wish to bridge
amoount | true | string | The amount you wish to bridge in ethereum units. See the [the token section](#tokens) section for how to convert this into nominal amounts.
signature | true | string | The signature of the account on this payload. See one of the code samples for how to do this.

### Response format

Name | Type | Description
--- | --- | ---
status | string | `success` or `failure` if the request succeeded or not. 



