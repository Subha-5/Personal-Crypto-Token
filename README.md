# Follow these below steps to initialize the project

(NOTE: Place or Copy the file to IC-PROJECT(your project folder) folder before running below steps)

1) -> In dfx.json file we can see the "dfx": "0.8.4" .

2) -> Now we have to downgrade our dfx version to 0.8.4 (this takes some time ~15mins) , Now to downgrade use the command

        DFX_VERSION=0.8.4 sh -ci "$(curl -fsSL https://smartcontracts.org/install.sh)"

3) ->After downgrading the dfx version, Now type

         $ dfx start --emulator

4) -> Now split the terminal and type

         $ npm install --legacy-peer-deps

(NOTE: Ignore the deprecated warning)

5) -> Now deploy

          $ dfx deploy

6) -> Now after this type

          $ npm start

(NOTE: Don't worry of downgrading the dfx version we can upgrade it back to latest version when needed)

(--->

ADDITIONAL SOLUTION FOR ERROR  IN dfx deploy

Error:  The replica returned an HTTP Error: Http Error: status 400 Bad Request for your canister

Solution: Just type
        `$ dfx start --clean`

<----)

# Check your Balance

1. Find out your principal id:

```
dfx identity get-principal
```

2. Save it somewhere.

e.g. My principal id is: d66ef-652qc-p4sw2-nevk4-hkj3w-hgihb-cliym-lzdjb-cl7ux-7tq6r-eqe


3. Format and store it in a command line variable:
```
OWNER_PUBLIC_KEY="principal \"$( \dfx identity get-principal )\""
```

4. Check that step 3 worked by printing it out:
```
echo $OWNER_PUBLIC_KEY
```

5. Check the owner's balance:
```
dfx canister call token balanceOf "( $OWNER_PUBLIC_KEY )"
```

# Charge the Canister


1. Check canister ID:
```
dfx canister id token
```

2. Save canister ID into a command line variable:
```
CANISTER_PUBLIC_KEY="principal \"$( \dfx canister id token )\""
```

3. Check canister ID has been successfully saved:
```
echo $CANISTER_PUBLIC_KEY
```

4. Transfer half a billion tokens to the canister Principal ID:
```
dfx canister call token transfer "($CANISTER_PUBLIC_KEY, 500_000_000)"
```

# Deploy the Project to the Live IC Network

1. Create and deploy canisters:

```
dfx deploy --network ic
```

2. Check the live canister ID:
```
dfx canister --network ic id token
```

3. Save the live canister ID to a command line variable:
```
LIVE_CANISTER_KEY="principal \"$( \dfx canister --network ic id token )\""
```

4. Check that it worked:
```
echo $LIVE_CANISTER_KEY
```

5. Transfer some tokens to the live canister:
```
dfx canister --network ic call token transfer "($LIVE_CANISTER_KEY, 50_000_000)"
```

6. Get live canister front-end id:
```
dfx canister --network ic id token_assets
```
7. Copy the id from step 6 and add .raw.ic0.app to the end to form a URL.
e.g. zdv65-7qaaa-aaaai-qibdq-cai.raw.ic0.app