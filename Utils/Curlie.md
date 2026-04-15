# Curlie

[curlie](https://github.com/rs/curlie) is a CLI HTTP client that gives you the ease of HTTPie with the power of `curl`. It essentially behaves as a frontend for `curl` while adopting the intuitive syntax of HTTPie.

## Core Features
- Full compatibility with `curl` flags.
- HTTPie-style simplified body and header parameters.
- Colorized and formatted output.

## Testing [[LM Studio]] with `curlie`

### List Models
```bash
curlie GET http://localhost:1234/v1/models
```

### Chat Completions
```bash
curlie POST http://localhost:1234/v1/chat/completions \
  model="local-model" \
  messages:='[{"role": "user", "content": "Hello!"}]'
```

### Text Completions
```bash
curlie POST http://localhost:1234/v1/completions \
  model="local-model" \
  prompt="Tell me a joke."
```

## Comparisons
- See also [[Xh]] for a high-performance Rust-based alternative.
