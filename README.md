# sn-local-testnet-action

Github Action for administering local testnets.

## Usage

### Start a Testnet

```
- name: Start a local network
  uses: maidsafe/sn-local-testnet-action@main
  with:
    action: start
    interval: 2000
    node-path: target/release/safenode
    faucet-path: target/release/faucet
    platform: ubuntu-latest
```
For other input options, see the `action.yml`.

You may want to consider causing your workflow to fail if the `SAFE_PEERS` variable was not set correctly:
```
- name: Check SAFE_PEERS was set
  shell: bash
  run: |
    if [[ -z "$SAFE_PEERS" ]]; then
      echo "The SAFE_PEERS variable has not been set"
      exit 1
    else
      echo "SAFE_PEERS has been set to $SAFE_PEERS"
    fi
```

### Stop a Testnet

```
- name: Stop the local network and upload logs
  if: always()
  uses: jacderida/sn-local-testnet-action@initial-testnet-admin
  with:
    action: stop
    log_file_prefix: safe_test_logs_e2e
    platform: ubuntu-latest
```
