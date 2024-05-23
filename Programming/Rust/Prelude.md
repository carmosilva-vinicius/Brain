Is a pre imported group of [[Rust]] objects from standard library, that are present at all projects.

- std::marker::{Copy, Send, Sized, Sync, Unpin}, marker traits that indicate fundamental properties of types.
- std::ops::{Drop, Fn, FnMut, FnOnce}, various operations for both destructors and overloading ().
- std::mem::drop, a convenience function for explicitly dropping a value.
- std::boxed::Box, a way to allocate values on the heap.
- std::borrow::ToOwned, the conversion trait that defines to_owned, the generic method for creating an owned type from a borrowed type.
- std::clone::Clone, the ubiquitous trait that defines clone, the method for producing a copy of a value.
- std::cmp::{PartialEq, PartialOrd, Eq, Ord}, the comparison traits, which implement the comparison operators and are often seen in trait bounds.
- std::convert::{AsRef, AsMut, Into, From}, generic conversions, used by savvy API authors to create overloaded methods.
- std::default::Default, types that have default values.
- std::iter::{Iterator, Extend, IntoIterator, DoubleEndedIterator, ExactSizeIterator}, iterators of various kinds.
- std::option::Option::{self, Some, None}, a type which expresses the presence or absence of a value. This type is so commonly used, its variants are also exported.
- std::result::Result::{self, Ok, Err}, a type for functions that may succeed or fail. Like Option, its variants are exported as well.
- std::string::{String, ToString}, heap-allocated strings.
- std::vec::Vec, a growable, heap-allocated vector.
- std::convert::{TryFrom, TryInto},
- std::iter::FromIterator.