# Rust Testing

## Defaults

- Unit tests in `mod tests`
- Integration tests in `tests/`
- Prefer `Result<()>` in tests when it improves readability

## Minimal examples

## Unit test

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn normalizes_email() {
        assert_eq!(normalize_email("A@B.COM"), "a@b.com");
    }
}
```

## Integration test

```rust
// tests/api_smoke.rs
#[test]
fn starts_and_responds() {
    // ...
}
```
