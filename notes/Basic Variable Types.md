# Basic Variable Types

## Integer

We have *signed* and *unsigned* integers:

| length | signed | unsigned |
| ------ | ------ | -------- |
| 8      | `i8`   | `u8`     |
| 16     | `i16`  | `u16`    |
| 32     | `i32`  | `u32`    |
| 64     | `i64`  | `u64`    |
| ...    | ...    | ...      |

### Integer Overflow

Rust checks integer overflow in debug mode. If overflow exists, the program will panic(i.e. the program exit due to the existence of error) during compilation.

We can use `--release` parameter to disable it, but the overflow may not happen as expected. 

- **We should never rely on the usage of overflow**

Useful methods to deal with overflow:

- `wrapping_*` All methods follows the rule of 2's complement wrapping, e.g.:
  
  ```rust
  fn main() {
      let a : u8 = 255;
      let b = a.wrapping_add(20);
      println!("{}", b);  // 19
  }
  ```

- `checked_*` Return `None` when overflow

- `overflowing_*` Return the value and a boolean value that check if there's an overflow

- `saturating_*` Return the maximum or minimum value of the variable



## Floating Numbers

We have `f32` and `f64` in Rust, the performance is nearly the same, but with difference on precision.

Notice that:

1. floating number is the **approximation** of the number you want to represent. E.g.:
   
   ```rust
   // the code below panic because of the error on float
   fn main() {
     assert!(0.1 + 0.2 == 0.3);
   }
   ```
   
   So if we want to compare two floats, we can use `(0.1_f64 + 0.2 - 0.3).abs() < 0.00001`

2. Some feature of floats are unimplemented, e.g.: floats use `std::cmp::PartialEq` for comparison rather than `std::cmp::PartialEq`. This means we cannot set a float as a key in `HashMap`.
