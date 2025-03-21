# metatype

[![Crates.io](https://img.shields.io/crates/v/metatype.svg?maxAge=86400)](https://crates.io/crates/metatype)
[![MIT / Apache 2.0 licensed](https://img.shields.io/crates/l/metatype.svg?maxAge=2592000)](#License)
[![Build Status](https://dev.azure.com/alecmocatta/metatype/_apis/build/status/tests?branchName=master)](https://dev.azure.com/alecmocatta/metatype/_build?definitionId=7)

[📖 Docs](https://docs.rs/metatype/0.2) | [💬 Chat](https://constellation.zulipchat.com/#narrow/stream/213236-subprojects)

Helper methods to determine whether a type is `TraitObject`, `Slice` or `Concrete`, and work with them respectively.

## Examples

```rust
assert_eq!(usize::METATYPE, MetaType::Concrete);
assert_eq!(any::Any::METATYPE, MetaType::TraitObject);
assert_eq!(<[u8]>::METATYPE, MetaType::Slice);

let a: Box<usize> = Box::new(123);
assert_eq!(Type::meta_type(&*a), MetaType::Concrete);
let a: Box<dyn any::Any> = a;
assert_eq!(Type::meta_type(&*a), MetaType::TraitObject);

let a = [123,456];
assert_eq!(Type::meta_type(&a), MetaType::Concrete);
let a: &[i32] = &a;
assert_eq!(Type::meta_type(a), MetaType::Slice);

let a: Box<dyn any::Any> = Box::new(123);
let meta: TraitObject = type_coerce(Type::meta(&*a));
println!("vtable: {:?}", meta.vtable);
```

## Note

This currently requires Rust nightly for the `ptr_metadata`, `specialization` and `arbitrary_self_types_pointers` features.

## License

Licensed under either of

 * Apache License, Version 2.0, ([LICENSE-APACHE.txt](LICENSE-APACHE.txt) or http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license ([LICENSE-MIT.txt](LICENSE-MIT.txt) or http://opensource.org/licenses/MIT)

at your option.

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in the work by you, as defined in the Apache-2.0 license, shall be dual licensed as above, without any additional terms or conditions.
