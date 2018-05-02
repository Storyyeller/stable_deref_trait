This crate defines an unsafe marker trait, StableDeref, for container types which deref to a fixed address which is valid even when the containing type is moved. For example, Box, Vec, Rc, Arc and String implement this trait. Additionally, it defines CloneStableDeref for types like Rc where clones deref to the same address.

It is intended to be used by crates such as [owning_ref](https://crates.io/crates/owning_ref) and [rental](https://crates.io/crates/rental), as well as library authors who wish to make their code interoperable with such crates. For example, if you write a custom Vec type, you can implement StableDeref, and then users will be able to use your custom Vec type together with owning_ref and rental.

no_std support can be enabled by disabling default features (specifically "std"). In this case, the trait will not be implemented for the std types mentioned above, but you can still use it for your own types.

Enable the "alloc" feature (with default-features disabled) to have this trait be implemented for the above types from the built-in `alloc` crate, specifically
* `alloc::boxed::Box`
* `alloc::vec::Vec`
* `alloc::rc::Rc`
* `alloc::arc::Arc`
* `alloc::string::String`

Enable the "spin_mutex" feature (with default-features disabled) to have this trait be implemented for the following types from the [spin](https://crates.io/crates/spin) crate:
* `spin::MutexGuard`
* `spin::RwLockReadGuard`
* `spin::RwLockWriteGuard`
