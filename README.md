# port-crates-to-rust-sgx-sdk

* About *std*

  Only support *std*

  1. Fix features:

     ```mermaid
     div
     ```
  2. Add headers in the lib.rs to enable the std. For example:

     ```mermaid
     div
     ```

  Both support *std* and *no_std*

  1. Fix features:
     ```mermaid
     [features]

     std = ["mesalock_sgx"]

     default = ["std", "mesalock_sgx"]

     mesalock_sgx = ["sgx_tstd", "std"]
     ```
  2. Add headers in the lib.rs to enable the std. For example:
     ```mermaid
     //#![cfg_attr(not(feature = "std"), no_std)]



     #![cfg_attr(not(

     all(

     any(feature = "std", feature = "mesalock_sgx"),

     target_env = "sgx",

     target_vendor = "mesalock",

     )),

     no_std

     )]



     #![cfg_attr(

     all(

     any(feature = "std", feature = "mesalock_sgx"),

     target_env = "sgx",

     target_vendor = "mesalock",

     ),

     feature(rustc_private)

     )]



     #[cfg(all(

     any(feature = "std", feature = "mesalock_sgx"),

     not(target_env = "sgx"),

     not(target_vendor = "mesalock"),

     ))]

     #[macro_use]

     extern crate sgx_tstd as std;
     ```

  About *core*

  1. If it is a *no_std* environment, you don't need to import "*extern crate core;*" explicitly;
  2. In the *use_std/std~~~~* environment, if you need to use the core library, you need to explicitly import the "*extern crate core;*".
