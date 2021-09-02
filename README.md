## WASM code migration tester

---

smart contract migration tester for Terra via LocaTerra

Migration is needed because there are some breaking changes for wasm contract between columbus-4 and columbus-5.

## Requirements

---

* [Docker](https://www.docker.com/) installed and configured on your system
* [`docker-compose`](https://github.com/docker/compose) ^1
* Supported known architecture: x86_64
* node.js >= 14

## Usage

---

### Columbus-4

Run columbus-4 and deploy(store code and instantiate contract) a contract.

  ```makefile
  make columbus-4
  ```

### Deploy contract on columbus-4

```bash
# place your wasm binary and its initMsg json file into ./contracts/columbus-4/ before run make
# set FILENAME_WASM as name of the binary
# set FILENAME_INITMSG as initMsg for the code ($(FILENAME_WASM.init.json) by default)
FILENAME_WASM=send_to_burn_address.wasm  FILENAME_INITMSG=s2ba.json make deploy_contract
# on success, see log/deployed.$(BLOCK_HEIGHT).log
```

### Bombay

Export columbus, run migrated columbus-5 and do migrateCode

It migrates code for send_to_burn_address.wasm for example.

  ```makefile
  make columbus-5
  ```

### Migrate code on columbus-5

```bash
# place your wasm binary into ./contracts/columbus-5/ before run make
# set FILENAME_WASM as name of the binary
# set CODE_ID to use
FILENAME_WASM=send_to_burn_address.wasm CODE_ID=1 make migrate_code
```

### Cleanup

Clean LocalTerra containers, temporary files and logs

```bash
make clean
```

---

## License

This software is licensed under the MIT license.

© 2020 Terraform Labs, PTE.
