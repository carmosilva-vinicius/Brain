# LM Studio

LM Studio is a desktop application that allows you to discover, download, and run local LLMs (Large Language Models) on your machine. It provides a local server that mimics the OpenAI API, making it easy to test models with standard HTTP clients.

## API Base URL
The default base URL for the local server is usually `http://localhost:1234/v1`.

## Key API Routes

- **List Models**
  - `GET /v1/models`
  - Returns a list of models currently loaded in LM Studio.

- **Get Responses**
  - `POST /v1/responses`
  - A route for generic model responses.

- **Chat Completions**
  - `POST /v1/chat/completions`
  - The standard route for chat-based interactions (OpenAI compatible).

- **Text Completions**
  - `POST /v1/completions`
  - Legacy text completion route.

- **Embeddings**
  - `POST /v1/embeddings`
  - Generates vector embeddings for a given text.

## Usage with HTTP Clients
You can test these routes using modern CLI tools like [[Xh]] and [[Curlie]].
