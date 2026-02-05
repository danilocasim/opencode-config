# Go Testing (testing)

## Defaults

- Table-driven tests
- `httptest` for HTTP handlers
- Avoid global state; use dependency injection

## Table test

```go
func TestNormalizeEmail(t *testing.T) {
  tests := []struct {
    name string
    in   string
    want string
  }{
    {"basic", "A@B.COM", "a@b.com"},
    {"trim", "  a@b.com ", "a@b.com"},
  }

  for _, tt := range tests {
    t.Run(tt.name, func(t *testing.T) {
      got := NormalizeEmail(tt.in)
      if got != tt.want {
        t.Fatalf("got %q want %q", got, tt.want)
      }
    })
  }
}
```

## HTTP handler

```go
req := httptest.NewRequest("GET", "/health", nil)
rr := httptest.NewRecorder()
handler.ServeHTTP(rr, req)
if rr.Code != http.StatusOK { t.Fatal(rr.Code) }
```
