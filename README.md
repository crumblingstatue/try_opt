Helper macro for unwrapping `Option` values while returning early with an
error if the value of the expression is `None`. Can only be used in
functions that return `Option` because of the early return of `None` that
it provides.

# Examples

```Rust
#[macro_use]
extern crate try_opt;

use std::collections::HashMap;

fn map_add_checked(map: &HashMap<&str, i32>, lhs: &str, rhs: &str) -> Option<i32> {
    let lhs = try_opt!(map.get(lhs));
    let rhs = try_opt!(map.get(rhs));
    lhs.checked_add(*rhs)
}

fn main() {
    let mut map = HashMap::new();
    map.insert("foo", 2);
    map.insert("bar", 4);
    map.insert("baz", 12);
    assert_eq!(map_add_checked(&map, "foo", "bar"), Some(6));
    assert_eq!(map_add_checked(&map, "baz", "qux"), None);
}
```
