# Rust

# Link
* [Video](https://www.youtube.com/watch?v=-lYeJeQ11OI&list=PLfllocyHVgsRwLkTAhG0E-2QxCf-ozBkk&pp=iAQB)
* [Document](https://dhghomon.github.io/easy_rust/)


# Installation
If you’re a Windows Subsystem for Linux user run the following in your terminal, then follow the on-screen instructions to install Rust.
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

## Configuring the PATH environment variable
In the Rust development environment, all tools are installed to the ~/.cargo/bin directory, and this is where you will find the Rust toolchain, including rustc, cargo, and rustup.

Accordingly, it is customary for Rust developers to include this directory in their PATH environment variable. During installation rustup will attempt to configure the PATH. Because of differences between platforms, command shells, and bugs in rustup, the modifications to PATH may not take effect until the console is restarted, or the user is logged out, or it may not succeed at all.

If, after installation, running rustc --version in the console fails, this is the most likely reason.

## Types
Rust has many types that let you work with numbers, characters, and so on. Some are simple, others are more complicated, and you can even create your own.

### Primitive types
Rust has simple types that are called primitive types (primitive = very basic). We will start with integers and char (characters). Integers are whole numbers with no decimal point. There are two types of integers:

* Signed integers,
* Unsigned integers.

Signed means + (plus sign) and - (minus sign), so signed integers can be positive or negative (e.g. +8, -8). But unsigned integers can only be positive, because they do not have a sign.

The signed integers are: i8, i16, i32, i64, i128, and isize. The unsigned integers are: u8, u16, u32, u64, u128, and usize.

The number after the i or the u means the number of bits for the number, so numbers with more bits can be larger. 8 bits = one byte, so i8 is one byte, i64 is 8 bytes, and so on. Number types with larger sizes can hold larger numbers. For example, a u8 can hold up to 255, but a u16 can hold up to 65535. And a u128 can hold up to 340282366920938463463374607431768211455.

So what is isize and usize? This means the number of bits on your type of computer. (The number of bits on your computer is called the architecture of your computer.) So isize and usize on a 32-bit computer is like i32 and u32, and isize and usize on a 64-bit computer is like i64 and u64.

So those are two reasons for all the different number types in Rust. Here is another reason: usize is the size that Rust uses for indexing. (Indexing means "which item is first", "which item is second", etc.) usize is the best size for indexing because:

* An index can't be negative, so it needs to be a number with a u
* It should be big, because sometimes you need to index many things, but
* It can't be a u64 because 32-bit computers can't use u64.
So Rust uses usize so that your computer can get the biggest number for indexing that it can read.

Let's learn some more about char. You saw that a char is always one character, and uses '' instead of "".

All chars use 4 bytes of memory, since 4 bytes are enough to hold any kind of character:

* Basic letters and symbols usually need 1 out of 4 bytes: a b 1 2 + - = $ @
* Other letters like German Umlauts or accents need 2 out of 4 bytes: ä ö ü ß è é à ñ
* Korean, Japanese or Chinese characters need 3 or 4 bytes: 国 안 녕
When using characters as part of a string, the string is encoded to use the least amount of memory needed for each character.

We can use .len() to see this for ourselves:
```
fn main() {
    println!("Size of a char: {}", std::mem::size_of::<char>()); // 4 bytes
    println!("Size of string containing 'a': {}", "a".len()); // .len() gives the size of the string in bytes
    println!("Size of string containing 'ß': {}", "ß".len());
    println!("Size of string containing '国': {}", "国".len());
    println!("Size of string containing '𓅱': {}", "𓅱".len());
}
```
This prints:
```
Size of a char: 4
Size of string containing 'a': 1
Size of string containing 'ß': 2
Size of string containing '国': 3
Size of string containing '𓅱': 4
```

You can see that a is one byte, the German ß is two, the Japanese 国 is three, and the ancient Egyptian 𓅱 is 4 bytes.

```
fn main() {
    let slice = "Hello!";
    println!("Slice is {} bytes.", slice.len());
    let slice2 = "안녕!"; // Korean for "hi"
    println!("Slice2 is {} bytes.", slice2.len());
}
This prints:
```
Slice is 6 bytes.
Slice2 is 7 bytes.
slice is 6 characters in length and 6 bytes, but slice2 is 3 characters in length and 7 bytes.
```

If .len() gives the size in bytes, what about the size in characters? We will learn about these methods later, but you can just remember that .chars().count() will do it. .chars().count() turns what you wrote into characters and then counts how many there are.

```
fn main() {
    let slice = "Hello!";
    println!("Slice is {} bytes and also {} characters.", slice.len(), slice.chars().count());
    let slice2 = "안녕!";
    println!("Slice2 is {} bytes but only {} characters.", slice2.len(), slice2.chars().count());
}
```

This prints:
```
Slice is 6 bytes and also 6 characters.
Slice2 is 7 bytes but only 3 characters.
```

