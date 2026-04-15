# Xh

[xh](https://github.com/ducaale/xh) is a friendly and fast tool for sending HTTP requests. It's written in Rust and provides a modern syntax similar to HTTPie, but with higher performance.

## Core Features
- Native support for JSON.
- Colorized output.
- Auto-completion for shell.
- Easy to use syntax.

## Testing [[LM Studio]] with `xh`

### List Models
```bash
xh GET http://localhost:1234/v1/models
```

### Chat Completions
```bash
xh POST http://localhost:1234/v1/chat/completions \
  model="local-model" \
  messages:='[{"role": "user", "content": "Hello!"}]'
```

### Generate Embeddings
```bash
xh POST http://localhost:1234/v1/embeddings \
  model="text-embedding-3-small" \
  input="The text to embed."
```

## Comparisons
- See also [[Curlie]] for a tool that combines curl with HTTPie ease.
