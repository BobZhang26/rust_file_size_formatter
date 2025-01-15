# Rust Lab: Create a File Size Formatter

## Learning Objectives:
- Understand how to define and use enums and structs in Rust.
- Practice error handling using match expressions and handling invalid input.
- Gain familiarity with string parsing and formatting in Rust.
- Learn how to implement the Debug trait to print debug information of a struct.
- Enhance code readability by leveraging Rust’s string formatting capabilities.

```rust
use std::env;

#[derive(Debug)]
struct FileSizes {
    bytes: String,
    kilobytes: String,
    megabytes: String,
    gigabytes: String,
}

impl FileSizes {
    fn from(input: &str) -> Result<Self, String> {
        let parts: Vec<&str> = input.split_whitespace().collect();
        if parts.len() != 2 {
            return Err("Invalid input. Please use the format '<number> <unit>'.".to_string());
        }

        let number: f64 = parts[0]
            .parse()
            .map_err(|_| "Invalid number.".to_string())?;
        let unit = parts[1].to_lowercase();

        let bytes = match unit.as_str() {
            "b" | "bytes" => number,
            "kb" | "kilobytes" => number * 1_000.0,
            "mb" | "megabytes" => number * 1_000_000.0,
            "gb" | "gigabytes" => number * 1_000_000_000.0,
            _ => return Err("Invalid unit. Use 'b', 'kb', 'mb', or 'gb'.".to_string()),
        };

        Ok(FileSizes {
            bytes: format!("{} bytes", bytes as u64),
            kilobytes: format!("{} kilobytes", bytes / 1_000.0),
            megabytes: format!("{} megabytes", bytes / 1_000_000.0),
            gigabytes: format!("{} gigabytes", bytes / 1_000_000_000.0),
        })
    }
}

fn main() {
    let args: Vec<String> = env::args().collect();
    if args.len() != 2 {
        eprintln!("Usage: cargo run \"<number> <unit>\"");
        return;
    }

    let input = &args[1];
    match FileSizes::from(input) {
        Ok(sizes) => {
            println!(
                "{{Bytes: {} , Kilobytes: {} , Megabytes: {} , Gigabytes: {}}}",
                sizes.bytes, sizes.kilobytes, sizes.megabytes, sizes.gigabytes
            );
        }
        Err(err) => eprintln!("Error: {}", err),
    }
}
```