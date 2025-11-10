# GLM-4.6-FP8 API Client - Hugging Face Inference API

Cliente oficial para acessar o modelo GLM-4.6-FP8 via Hugging Face Inference API. Sem deploy necessario!

## Caracteristicas

- API HTTP pura - sem instalacao complexa
- Multiplas linguagens: Python, JavaScript, cURL, Go, Rust, PHP
- Zero deployment - use direto via Hugging Face
- Modelo GLM-4.6-FP8 (358B parametros, quantizado)
- Producao-ready com tratamento de erros

## Setup Rapido

### 1. Token Hugging Face

```bash
https://huggingface.co/settings/tokens
```

### 2. Clone

```bash
git clone https://github.com/OARANHA/GLM-4.6-FP8-API-Client
```

## Exemplos de Uso

### Python

```python
import requests

API_URL = "https://api-inference.huggingface.co/models/zai-org/GLM-4.6-FP8"
token = "seu_token_aqui"

headers = {"Authorization": f"Bearer {token}"}
payload = {"inputs": "Ola, como voce esta?"}

response = requests.post(API_URL, headers=headers, json=payload)
print(response.json())
```

### JavaScript

```javascript
const token = process.env.HUGGINGFACE_TOKEN;

const response = await fetch(
    "https://api-inference.huggingface.co/models/zai-org/GLM-4.6-FP8",
    {
        headers: { Authorization: `Bearer ${token}` },
        method: "POST",
        body: JSON.stringify({inputs: "Ola, como voce esta?"}),
    }
);

const result = await response.json();
console.log(result);
```

### cURL

```bash
curl https://api-inference.huggingface.co/models/zai-org/GLM-4.6-FP8 \
  -X POST \
  -H "Authorization: Bearer $HF_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"inputs":"Ola, como voce esta?"}'
```

### Go

```go
package main

import (
	"bytes"
	"encoding/json"
	"fmt"
	"io/ioutil"
	"net/http"
	"os"
)

func main() {
	token := os.Getenv("HUGGINGFACE_TOKEN")
	payload := map[string]string{"inputs": "Ola, como voce esta?"}
	payloadBytes, _ := json.Marshal(payload)

	req, _ := http.NewRequest("POST",
		"https://api-inference.huggingface.co/models/zai-org/GLM-4.6-FP8",
		bytes.NewBuffer(payloadBytes))
	req.Header.Set("Authorization", fmt.Sprintf("Bearer %s", token))
	req.Header.Set("Content-Type", "application/json")

	client := &http.Client{}
	resp, _ := client.Do(req)
	defer resp.Body.Close()
	body, _ := ioutil.ReadAll(resp.Body)
	fmt.Println(string(body))
}
```

### Rust

```rust
use reqwest;
use serde_json::json;

#[tokio::main]
async fn main() {
    let token = std::env::var("HUGGINGFACE_TOKEN").unwrap();
    let client = reqwest::Client::new();
    
    let response = client
        .post("https://api-inference.huggingface.co/models/zai-org/GLM-4.6-FP8")
        .header("Authorization", format!("Bearer {}", token))
        .json(&json!({"inputs": "Ola, como voce esta?"}))
        .send()
        .await
        .unwrap();

    let body = response.text().await.unwrap();
    println!("{}", body);
}
```

### PHP

```php
<?php
$token = getenv('HUGGINGFACE_TOKEN');
$url = 'https://api-inference.huggingface.co/models/zai-org/GLM-4.6-FP8';

$data = json_encode(['inputs' => 'Ola, como voce esta?']);

$options = stream_context_create([
    'http' => [
        'header' => [
            'Authorization: Bearer ' . $token,
            'Content-Type: application/json'
        ],
        'method' => 'POST',
        'content' => $data
    ]
]);

$response = file_get_contents($url, false, $options);
echo $response;
```

## Parametros

- `inputs`: texto de entrada
- `parameters.max_new_tokens`: tokens max
- `parameters.temperature`: criatividade
- `parameters.top_p`: nucleus sampling

## Variavel de Ambiente

```bash
export HUGGINGFACE_TOKEN="hf_xxxxxxxxxxxxx"
```

## Referencias

- [GLM-4.6-FP8](https://huggingface.co/zai-org/GLM-4.6-FP8)
- [Hugging Face Inference API](https://huggingface.co/docs/api-inference)
- [Zhipu AI](https://z.ai/)

## Licenca

MIT License
