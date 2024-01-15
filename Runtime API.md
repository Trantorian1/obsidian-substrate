
> 📚 A **runtime API** in substrate is a bridge between the outer nodes services (ie: the services listening and responding to other nodes in the network) and the node runtime.
> This is to say outer request and responses need to be able to interact on a business logic level with local data such as the node database. This is achieved through [runtime APIs](https://docs.substrate.io/reference/runtime-apis/).

---
# Defining a Runtime

Substrate runtimes are defined using the `decl_runtime_apis!` macro. A single runtime can be defined per module, and ca be split into traits.

> 📚 **Runtime traits** are simple rust traits defined within a substrate runtime API and can be seen as runtime modules, allowing for a better grouping of runtime functionalities.

*ex:*
```rust
sp_api::decl_runtime_apis! {
    /// Declare the api trait.
    pub trait Balance {
        /// Get the balance.
        fn get_balance() -> u64;
        /// Set the balance.
        fn set_balance(val: u64);
    }

    /// You can declare multiple api traits in one macro call.
    /// In one module you can call the macro at maximum one time.
    pub trait BlockBuilder {
        /// The macro adds an explicit `Block: BlockT` generic parameter for you.
        /// You can use this generic parameter as you would defined it manually.
        fn build_block() -> Block;
    }
}
```
*from the sp_api [crate documentation](https://paritytech.github.io/polkadot-sdk/master/sp_api/macro.decl_runtime_apis.html#example)*

---
# Implementing a Runtime

Once a runtime has been created using `decl_runtime_apis`, the implementations of the functions declared for each of it's traits needs to be provided. This is achieved via the `impl_runtime_apis!` macro.

*ex:*
```rust
impl_runtime_apis! {
    impl self::Balance<Block> for Runtime {
        /// Returns a fixed dummy balance.
        fn get_balance() -> u64 {
            1000
        }

        /// Sets a new balance.
        fn set_balance(val: u64) {
            // ...
        }
    }

    /// Implement the BlockBuilder runtime API
    impl self::BlockBuilder<Block> for Runtime {
        /// Builds and returns a dummy block.
        fn build_block() -> Block {
			// ...
        }
    }
}
```