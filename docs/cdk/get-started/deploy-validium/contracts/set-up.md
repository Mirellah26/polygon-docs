## Download the validium repo

1. Create a new directory and cd into it.

    ```bash
    cd ~/
    mkdir cdk-validium
    cd cdk-validium/
    ```

2. Download the `0.0.2` release from the [cdk-validium-contracts github repo](https://github.com/0xPolygon/cdk-validium-contracts/releases/tag/v0.0.2-RC1).

    !!! note
        The download is available in both `.tar.gz` and `.zip` formats.

    ```bash
    curl -L -o cdk-validium-contracts.tar.gz https://github.com/0xPolygon/cdk-validium-contracts/archive/refs/tags/v0.0.2.tar.gz
    ```

3. Extract the files and cd into the repo.

    ```bash
    tar -xzf cdk-validium-contracts.tar.gz
    cd cdk-validium-contracts-0.0.2/
    ```

## Install the dependencies

```bash
npm install
```

## Create the .env configuration

1. Copy the environment configuration example file into a new `.env` file.

    ```bash
    cp .env.example .env
    ```

2. Generate a new mnemonic using `cast`.

    ```bash
    cast wallet new-mnemonic --words 12
    ```

    !!! tip
        If the command `new-mnemonic` is not found, update foundry with `foundryup` and try again.

    The output should look something like this:

    ```bash
    Phrase:
    island debris exhaust typical clap debate exhaust little verify mean sausage entire
    Accounts:
    - Account 0:
    Address:     0x8Ea797e7f349dA91078B1d833C534D2c392BB7FE
    Private key: 0x3b01870a8449ada951f59c0275670bea1fc145954ee7cb1d46f7d21533600726
    ```

3. Add the environment variables to the `.env` file.

    ```bash
    nano .env
    MNEMONIC="<generated mnemonic>"  # copy/paste the generated Phrase
    INFURA_PROJECT_ID="<INFURA_PROJECT_ID>"  # Generate a project id on [Infura](https://www.infura.io/)
    ETHERSCAN_API_KEY="<ETHERSCAN_API_KEY>" # Generate an API key on [Etherscan](https://etherscan.io)
    ```

    !!! info
        Check our documentation if you want to [use a different node provider](deploy-contracts.md#use-a-different-node-provider).

4. Send 2 Sepolia ETH to the generated address.

5. Add the following variables to `/var/tmp/cdk/.env`. 

    ```bash
    nano /tmp/cdk/.env
    TEST_ADDRESS="<the address generated by cast>"
    TEST_PRIVATE_KEY="<the private key generated by cast>" 
    L1_URL="https://sepolia.infura.io/v3/<YOUR INFURA PROJECT ID>"
    L1_WS_URL="wss://sepolia.infura.io/ws/v3/<YOUR INFURA PROJECT ID>"
    ```
!!! important
    This step allows us to use `jq` and `tomlq` later on to setup our configuration files.

