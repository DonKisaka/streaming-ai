# Streaming AI Chat API

A reactive streaming AI chat API built with Spring Boot 4, Spring AI, and Ollama.

## Tech Stack

- Java 25
- Spring Boot 4.0.6
- Spring AI 1.1.5
- Spring WebFlux (reactive, non-blocking)
- Ollama (local AI model runner)
- Server-Sent Events (SSE)

## Prerequisites

- Java 25 installed
- [Ollama](https://ollama.com) installed and running

## Setup

**1. Start Ollama**
```bash
ollama serve
```

**2. Pull the model**
```bash
ollama pull llama3.2
```

**3. Run the app**
```bash
./mvnw spring-boot:run
```

## Usage

Send a GET request to the streaming endpoint:

```bash
curl -N -H "Accept: text/event-stream" "http://localhost:8080/chat/stream?message=What is Java?"
```

Or via Postman:
- Method: `GET`
- URL: `http://localhost:8080/chat/stream?message=Hello`
- Header: `Accept: text/event-stream`

## Configuration

`src/main/resources/application.properties`

```properties
spring.application.name=streaming-ai
spring.ai.ollama.base-url=http://localhost:11434
spring.ai.ollama.chat.options.model=llama3.2
server.port=8080
```

## How It Works

The `/chat/stream` endpoint returns a `Flux<String>` — tokens are streamed one by one as Ollama generates them, instead of waiting for the full response.
