> ⚠️ Storage querying (read/write) in Substrate is **expensive** and should be done sparingly. Data storage should be minimal and hashed, and data retrieval should be as sparse as possible to avoid too significant of an overhead.

---
# Storage types

There are four types of storage in Substrate:
- Single value storage
- Single key to single value storage
- Double key to single value storage
- Multi-key to single value storage

---
# Storage return types

> ℹ️ Storage return type needs to be specified explicitly as part of [[#Declaring Storage]]

Substrate allows the following return types for data stored in storage.

| Storage return type | Potential values        |
| ------------------- | ----------------------- |
| `OptionQuery`       | `Some(value)` or `None` |
| `ResultQuery`       | `Ok()value` or `Err`    |
| `ValueQuery`        | `value`                        |

---
# Declaring Storage

 Storage is declared using the `#[pallet::storage]` macro, with the following syntax:

## Single value storage

```rust
#[pallet::storage]
#[pallet::getter(fn some_value)]
type SomePrivateValue<T> = StorageValue<
    _,
    u32,       // value
    ValueQuery // return type
>;
```

## Single key to single value storage

```rust
#[pallet::storage]
#[pallet::getter(fn some_map)]
pub(super) type SomeMap<T: Config> = StorageMap<
    _,
    Blake2_128Concat, T::AccountId, // key
    u32,                            // value
    ValueQuery                      // return type
>;
```

## Double key to single value storage

```rust
#[pallet::storage]
#[pallet::getter(fn some_dmap)]
pub(super) type SomeDoubleMap<T: Config> = StorageDoubleMap<
    _,
    Blake2_128Concat, u32,          // key1
    Blake2_128Concat, T::AccountId, // key2
    u32,                            // value
    ValueQuery                      // return type
>;
```

## Multi-key to single value storage

```rust
#[pallet::storage]
#[pallet::getter(fn some_nmap)]
pub(super) type SomeNMap<T: Config> = StorageNMap<
    _,
    (   // keys
        NMapKey<Blake2_128Concat, u32>,
        NMapKey<Blake2_128Concat, T::AccountId>,
        NMapKey<Twox64Concat, u32>,
    ),
    u32, //values
    ValueQuery, // return type
>;
```