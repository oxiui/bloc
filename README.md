# Bloc (Business Logic Component) 

Bloc is a library for building scalable and maintainable business logic. 

This crate currently only exposes the [EnumHandler](https://crates.io/crates/enum_handler) derive marcro.

```rust
// You declare the CounterEvent enum:

use bloc::EnumHandler;

#[derive(EnumHandler)]
pub enum CounterEvent {
    Increment,
    Decrement,
    Reset,
    Set(i32),
}

// you can implement the CounterEventHandler trait for your struct:

pub struct Counter;

impl CounterEventHandler for Counter {
    fn on_increment(&self) {
        println!("Increment");
    }
    fn on_decrement(&self) {
        println!("Decrement");
    }
    fn on_reset(&self) {
        println!("Reset");
    }
    fn on_set(&self, set: i32) {
        println!("Set: {}", set);
    }
}


```

```rust ignore
// and the enum_handler macro will generate the following code for you behind the scenes:

pub trait CounterEventHandler {
    fn on(&self, e: CounterEvent) -> () {
        match (e) {
            CounterEvent::Increment => self.on_increment(),
            CounterEvent::Decrement => self.on_decrement(),
            CounterEvent::Reset => self.on_reset(),
            CounterEvent::Set(arg) => self.on_set(arg),
        }
    }
    fn on_increment(&self) -> ();
    fn on_decrement(&self) -> ();
    fn on_reset(&self) -> ();
    fn on_set(&self, set: i32) -> ();
}
```

## License

Licensed under either of

* Apache License, Version 2.0, ([LICENSE-APACHE](LICENSE-APACHE) or <http://www.apache.org/licenses/LICENSE-2.0>)
* MIT license ([LICENSE-MIT](LICENSE-MIT) or <http://opensource.org/licenses/MIT>)

at your option.
