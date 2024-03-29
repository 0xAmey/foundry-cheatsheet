- `forge build` - compile contracts
- `forge test` - run all tests (files with .t in them in which the functions starting with the word test are run)
- `forge test -vvvvv` - each v adds more information about the tests ran
- `forge test --match-contract <contract name> --match-test <keywords>` - runs the tests for the specified contract containing the keyword mentioned
- `forge test --match-path <path>` - another way to run tests 
- `test` functions with 
- `testFail` if the transaction doesn't revert the test fails
- Note: Test functions must have `external` or `public` visibility 
- `vm.prank(address(0x1))` - Prank as a user 
- `vm.expectRevert(errorName.selector)` - Expect transaction to revert with a specific error
- expectEmit
    - Expecting the emit to compare the event emitted by test and event emitted by contract. Can set value true if you want the values of both events to match (Note: need to _always_ give 4 bool values) 
    - `vm.expectEmit(bool, bool, bool, bool)`
    - `emit Event()`
    - `contract.call()`
- `stdMath` to access math library 
- Test trace colors: 
    - **Green**: For calls that do not revert
    - **Red**: For reverting calls
    - **Blue**: For calls to cheat codes
    - **Cyan**: For emitted logs
    - **Yellow**: For contract deployments
- Fork Testing
    - Forking Mode:
        - `forge test --fork-url <your_rpc_url>`
    - Forking Cheatcodes:
        - `forkId = vm.createFork(rpc_url, block_number)`
        - `vm.selectFork(forkId)`
        - Does the same thing but in a single line:
            - `vm.createSelectFork(rpc_url)`
- Fuzz Testing
    - `vm.assume(condition)`
    - example
        - `vm.assume(amount > 0.1 ether)`
- Deploy
    - forge can deploy only one contract at a time
    - `forge create --rpc-url <your_rpc_url> \
    --constructor-args "ForgeUSD" "FUSD" 18 1000000000000000000000 \
    --private-key <your_private_key> src/MyToken.sol:MyToken \
    --etherscan-api-key <your_etherscan_api_key> \
    --verify`
    - 
- Gas Reports
    - For specific contracts
        - `gas_reports = ["MyContract", "MyContractFactory"]`
    - For all
        - `gas_reports = ["*"]`
    - To generate run, `forge test --gas-report`
- Debugger
    - To enter debug mode 
        - `forge debug --debug src/SomeContract.sol --sig "myFunc(uint256,string)" 123 "hello"`
    - To  debug tests
        - `forge test --debug "testSomething"`
    - For memory 
        - **Red words** are about to be written to by the current opcode
        - **Green words** were written to by the previous opcode
        - **Cyan words** are being read by the current opcode
    - For Stack
        - **Cyan words** are either being read or popped by the current opcode.

- Cast
    - `cast <subcommand>`
- Anvil
    - Local testnet node
    - simply type `anvil`
- Setting environment variables (examples)
    - `export RPC_URL=<Your RPC endpoint>`
    - `export PRIVATE_KEY=<Your wallets private key>`
