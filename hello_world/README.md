# Hello World Tutorial

1. Start by running my local Solana node
```bash
solana-test-validator
```

2. Create a new project
```bash
cargo new hello-world --lib
```

3. Add the Solana dependency to the project
```bash
cd hello-world
cargo add solana-program
```
Check the `Cargo.toml` file to make sure the dependency was added correctly.
Make sure to add:
```toml
[lib]
name = "hello_world"
crate-type = ["cdylib", "lib"]
```

4. Add the Solana program code
```rust
use solana_program::{
    account_info::AccountInfo, entrypoint, entrypoint::ProgramResult, pubkey::Pubkey,
};

entrypoint!(process_instruction);

fn process_instruction(
    _program_id: &Pubkey,
    _accounts: &[AccountInfo],
    _instruction_data: &[u8],
) -> ProgramResult {
    Ok(())
}
```

5. Build the program
```bash
cargo build-bpf
```

6. Deploy the program
```bash
solana program deploy target/deploy/hello_world.so
```

7. Call the program
```bash
solana program call hello_world
```