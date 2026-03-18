# Spring AI RAG (Ollama, Java 25)

Spring Boot 3.5 + Spring AI ile Ollama üzerinden **RAG** (Retrieval Augmented Generation) örneği.  
Tüm sohbet istekleri `QuestionAnswerAdvisor` ile vektör deposundan bağlam çekerek modele gider.

## Gereksinimler

- **JDK 25** (Gradle toolchain ile otomatik eşleştirilebilir)
- [Ollama](https://ollama.com/) çalışır durumda (`ollama serve`)

## Ollama modelleri

```bash
ollama pull llama3.2
ollama pull nomic-embed-text
```

Chat ve embedding modellerini [`application.yml`](src/main/resources/application.yml) içinden değiştirebilirsiniz.

## Çalıştırma

```bash
./gradlew bootRun
```

Uygulama: `http://localhost:8080`

## API

**POST** `/api/chat`  
JSON gövde: `{ "message": "..." }`  
Yanıt: `{ "reply": "..." }`

Örnek:

```bash
curl -s -X POST http://localhost:8080/api/chat \
  -H "Content-Type: application/json" \
  -d '{"message":"Acme RAG Demo destek kanalı nedir?"}'
```

## Bilgi tabanı

Örnek metin [`src/main/resources/kb/knowledge-base.txt`](src/main/resources/kb/knowledge-base.txt) dosyasındadır. Uygulama açılışında bu metin embedding ile indekslenir. İçeriği güncelledikten sonra uygulamayı yeniden başlatın.

## Yapılandırma

| Özellik | Konum |
|--------|--------|
| Ollama URL, chat/embedding modelleri | `spring.ai.ollama.*` |
| RAG `topK` ve benzerlik eşiği | `app.rag.top-k`, `app.rag.similarity-threshold` |

## Derleme

```bash
./gradlew build
```
