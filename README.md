# API Encomendas - Desafio TecnoJr

API REST desenvolvida em Python com Flask e SQLite.

## Requisitos

- Python 3.10 ou superior
- pip

## Instalação

No terminal, dentro da pasta do projeto:

```bash
python -m venv venv
```

### Windows

```bash
venv\Scripts\activate
```

### Linux/macOS

```bash
source venv/bin/activate
```

Depois:

```bash
pip install -r requirements.txt
```

## Executar

```bash
python app.py
```

A API ficará disponível em:

```text
http://127.0.0.1:5000
```

O arquivo `encomendas.db` será criado automaticamente na primeira execução.

## Rotas

| Método |       Rota         |       Função         |
|--------|--------------------|----------------------|
|  POST  | `/encomendas`      | Criar encomenda      |
|  GET   | `/encomendas`      | Listar encomendas    |
|  GET   | `/encomendas/<id>` | Buscar uma encomenda |
|  PUT   | `/encomendas/<id>` | Atualizar encomenda  |
| DELETE | `/encomendas/<id>` | Remover encomenda    |

## Exemplo de POST

```json
{
  "nome_cliente": "Ana",
  "telefone": "73999999999",
  "produto": "Bolo de chocolate",
  "data_entrega": "2026-11-05",
  "status": "recebida"
}
```

O campo `status` aceita:

- `recebida`
- `em preparo`
- `entregue`

Se o status não for informado na criação, será usado `recebida`.

## Regra do bônus

A API impede a criação de mais de **5 encomendas para a mesma data**.

Se já houver 5 encomendas em uma determinada data, uma sexta tentativa retorna HTTP `409`.

A mesma regra é aplicada quando uma encomenda é atualizada para outra data.

## Testando com curl

Criar:

```bash
curl -X POST http://127.0.0.1:5000/encomendas \
-H "Content-Type: application/json" \
-d "{\"nome_cliente\":\"Ana\",\"telefone\":\"73999999999\",\"produto\":\"Bolo de chocolate\",\"data_entrega\":\"2026-11-05\",\"status\":\"recebida\"}"
```

Listar:

```bash
curl http://127.0.0.1:5000/encomendas
```

Atualizar:

```bash
curl -X PUT http://127.0.0.1:5000/encomendas/1 \
-H "Content-Type: application/json" \
-d "{\"status\":\"em preparo\"}"
```

Remover:

```bash
curl -X DELETE http://127.0.0.1:5000/encomendas/1
```
