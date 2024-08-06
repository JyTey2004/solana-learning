# Creating a token on Solana using Token 2022 Program

1. Create a keypair for the mint authority, then check if the json file named after the public key is created in the root directory.
```bash
# 1 keypair where the public key starts with bos
solana-keygen grind --starts-with bos:1
```

2. Configure the Solana CLI to use to use the keypair we just created:
```bash
# Change the keypair to the one we just created
solana config set --keypair bosy1VC2BH2gh5fdXA3oKn53EuATLwapLWC4VR2sGHJ.json
```

3. We will also set the Solana CLI to use devnet:
```bash
# Set the Solana CLI to use devnet
solana config set --url devnet
# Double check if the Solana CLI is set to devnet
solana config get
```

4. Get some Devnet SOL for the mint authority Account:
```bash
# Get the address of the mint authority account
solana address
```
Go to [https://faucet.solana.com/](https://faucet.solana.com/) and paste the address of the mint authority account to get some Devnet SOL.

5. Make a Mint Address with `mnt` as the prefix:
```bash
solana-keygen grind --starts-with mnt:1
```

6. Creating the token mint account:
Now, we will create the token mint, specifying to use the Token Extensions Program (TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb), with the metadata extension enabled.
```bash
# Create the token mint account, replace the mint account with the one you just created
spl-token create-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb --enable-metadata mntTymSqMU4e1NEDdxJ9XoPN4MitCgQ7xxGW6AuRAWQ.json
```

7. Create and upload image and offchain metadata over here we will use github as the source of the image and metadata, have a link that points to the image and metadata. 
Example metadata.json:
```json
{
  "name": "Example Token",
  "symbol": "EXMPL",
  "description": "Example token from Solana Making a Token guide.",
  "image": "https://raw.githubusercontent.com/solana-developers/opos-asset/main/assets/CompressedCoil/image.png"
}
```
Something like this:
```bash
https://raw.githubusercontent.com/JyTey2004/solana-learning/main/creating_a_token/metadata.json
```


8. Add the metadata to the token :
```bash
# Replace the token mint account with the one you just created
spl-token initialize-metadata mntTymSqMU4e1NEDdxJ9XoPN4MitCgQ7xxGW6AuRAWQ 'Example token' 'EXMPL' https://raw.githubusercontent.com/JyTey2004/solana-learning/main/creating_a_token/metadata.json

```

9. Now we can see the token in [Solana Explorer](https://explorer.solana.com/address/mntTymSqMU4e1NEDdxJ9XoPN4MitCgQ7xxGW6AuRAWQ?cluster=devnet)

10. Minting the token:

    a. First we need to create a token account to hold the tokens for our token mint:
    ```bash
    # Replace the token mint account with the one you just created
    spl-token create-account mntTymSqMU4e1NEDdxJ9XoPN4MitCgQ7xxGW6AuRAWQ
    ```

    b. Mint the token:
    ```bash
    # Replace the token mint account with the one you just created
    spl-token mint mntTymSqMU4e1NEDdxJ9XoPN4MitCgQ7xxGW6AuRAWQ 100
    ```

    c. Check the token account balance in Solana Explorer

11. Transfer the token to another account:
```bash
# Replace the token mint account with the one you just created
spl-token transfer mntTymSqMU4e1NEDdxJ9XoPN4MitCgQ7xxGW6AuRAWQ 10 (recipient wallet address) --fund-recipient
```