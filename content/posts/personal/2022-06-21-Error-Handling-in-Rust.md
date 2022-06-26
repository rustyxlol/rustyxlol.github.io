---
title: "Error Handling in Rust"
date: "2022-06-24"
description: &desc "Expressing errors, propagating them and creating custom error types."
summary: *desc
tags: ["personal"]
showToC: true
---

I recently started learning Rust and faced my biggest obstacle: Errors.  
I've mostly avoided error handling because it honestly didn't make any sense,
if you're the one writing code, then write it in a way that you won't have to
handle errors, why go the extra mile to handle them?  
Terrible. Terrible idea.  

Every popular builtin/library that you use contains a lot of error handling
mechanisms which help you decide what to do when an error is returned.  

For example, in Rust, when you try to add {integer} and {float},
you get an [error](https://doc.rust-lang.org/stable/error-index.html#E0277).
It may not be a serious problem in other languages but Rust takes it very
seriously, and rightfully so.  

This brings me to questioning the difference between exceptions and errors,
coming from Python, exceptions are basically events that disrupt the normal
flow of a program.  

For example, if you ask user for a numerical input but the user inputs a character,
or a string, then you are bound to get a `ValueError`.  

Now exceptions can be easily handled by anticipating what may or may not happen
given a certain scenario i.e., they are recoverable.  
But errors are pesky little things that may or may not be recoverable.  

The thing to keep in mind is, recoverable errors allow retrying an operation after
perhaps reporting it. *file not found* error is one such example.  
Unrecoverable errors are likely due to you, trying to access an out of bounds index,
that's bad. So we would want to immediately terminate the program if that happens.
> Rust requires you to acknowledge the possibility of an error and take some action
> before your code will compile.[^1]

## Unrecoverable errors

Rust has a macro for situations where you know that the recovery impossible or the
code is faulty.  
The panic macro essentially unwinds, i.e., going back and cleaning up.  

For example:[^2]  

```rs
fn main() {
    panic!("crash and burn");
}
```  

will generate the following:  

```bash
$ cargo run
   Compiling panic v0.1.0 (file:///projects/panic)
    Finished dev [unoptimized + debuginfo] target(s) in 0.25s
     Running `target/debug/panic`
thread 'main' panicked at 'crash and burn', src/main.rs:2:5
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```  

Using the `RUST_BACKTRACE=1` before `cargo run` will provide a flow of sorts which
will help you find out which one of your files caused the program to panic.  

Some other examples such as trying to access an invalid index in an array/vector will
also cause the program to panic.

Now while this is nice, where must one use this `panic!` macro?  
Generally, you will use panics in development environment, that includes testing,
demonstration and the like. There are methods that will panic for you, `unwrap` method
is one such example.  
> .unwrap() is "hey, I already know that this cannot fail, so just trust me"  
> — dawnofmidnight[^3]

## Recoverable Errors

Hang on tight because this is a big one, and a very deep one.  

Let's warmup with what we've learned so far about the `Result` enum and work our way
up to custom error types.  

Looking at Result's documentation, we see that it implemented as:  

```rs
pub enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

It has two variants, `Ok(T)` upon success and `Err(E)` upon failure. It essentially
"contains" our results.

Let's check it out with a quick example[^4]:

```rs
pub fn generate_nametag_text(name: String) -> ??? {
    if name.len() > 0 {
        ???
    } else {
        ???
    }
}
```

I'm sure the sentiment of the code is pretty clear, return something positive when
a `name` is inserted and perhaps an error mentioning that no name was inserted.  
This is the exact scenario where you would use `Result`.  

To be more descriptive, let us return `String` upon both success and failure.  
We could do it like so:  

```rs
pub fn generate_nametag_text(name: String) -> String {
    if name.len() > 0 {
        return format!("We got a name: {}", name);
    } else {
        return "We did not get a name!!".to_string();
    }
}
```

While this is very nice and does the job perfectly by fulfilling our requirements, it
doesn't provide much control to the function calling `generate_nametag_text`, how should
the calling function determine whether it was a success or a failure? By comparing the
entire string?  
What if a developer decides that, oh no, maybe the error message had an extra `!`
so I should probably remove it, and the whole code breaks because it depends on that one character.  

That is not very nice, which introduces us to `Result` enum, which could return an `Ok` if
a condition was satsified, `Err` or an error otherwise.  

And so, our program can be rewritten like:  

```rs
pub fn generate_nametag_text(name: String) -> Result<String, String> {
    if name.len() > 0 {
        return Ok(format!("We got a name: {}", name));
    } else {
        return Err("We did not get a name!!".to_string());
    }
}
```

Now the function will return a `Result` enum, which is essentially either
`Ok` or `Err` along with the exact same message, so now the caller of
`generate_nametag_text` doesn't have to depend on every character of the
message/string, but rather, can work with `Ok` and `Err`, which provides a lot better
control than returning a measly string.  

**TODO: Propagating Errors**

> basically~ use Result<T, E> if you can recover, and panic! when you cannot (and for tests)  
> — dawnofmidnight[^5]

[^1]: [Rust Book Chapter 9: Error Handling](https://doc.rust-lang.org/book/ch09-00-error-handling.html)
[^2]: [Rust Book Chapter 9.1: Unrecoverable Errors with panic](https://doc.rust-lang.org/book/ch09-01-unrecoverable-errors-with-panic.html#unrecoverable-errors-with-panic)
[^3]: [This quote is from dawn#4323 on Python Discord](https://discord.com/channels/267624335836053506/291284109232308226/987730661668454430)
[^4]: [This snippet is from rustlings error handling exercise, error1.rs](https://github.com/rust-lang/rustlings/blob/main/exercises/error_handling/errors1.rs)
[^5]: [This quote is also from dawn#4323 on Python Discord](https://discord.com/channels/267624335836053506/291284109232308226/987730494730936351)
