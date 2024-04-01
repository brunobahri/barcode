# Documentação para API Criadora de código de barras.

### Visão Geral

A API Criadora de de código de barras permite a criação de tags de códigos de barras para produtos. A API é projetada para receber um código de produto e retornar o caminho para a imagem da tag de código de barras gerada.

### Pré-requisitos
Para executar esta API localmente, você precisará ter:

Python 3.6 ou superior
pip (gerenciador de pacotes Python)

### Instalação

Clone o repositório do GitHub:

git clone https://github.com/brunobahri/barcode.git
cd barcode

Instale as dependências usando pip:

```pip install -r requirements.txt```
Inicie o servidor localmente:

python run.py


### Tratamento de Erros
Os erros são retornados como objetos JSON no formato a seguir:
```
{
  "errors": [
    {
      "title": "Título do Erro",
      "detail": "Uma mensagem detalhada do erro."
    }
  ]
} 
```
A API utiliza os seguintes códigos de erro:

422 Unprocessable Entity: Validação da entrada falhou.
500 Internal Server Error: Ocorreu um erro no servidor.

### Endpoints

POST /create_tag

Cria uma tag de código de barras para um determinado código de produto.

Requisição
URL: /create_tag
Método: POST
Headers:
Content-Type: application/json
Corpo:

```
{
  "product_code": "string"
}
```
### Parâmetros:

product_code (string, obrigatório): O código do produto para gerar a tag.
Resposta
Código de Status: 200 OK em sucesso, 422 Unprocessable Entity em erro de validação, 500 Internal Server Error em erros do servidor.

Corpo (em sucesso):

```
{
  "data": {
    "type": "Imagem da Tag",
    "count": 1,
    "path": "<caminho-para-codigo-de-barras-gerado>.png"
  }
}
```
A resposta inclui o tipo de dado retornado, a contagem de itens e o caminho para a imagem da tag gerada.

Corpo (em erro): Consulte a seção Tratamento de Erros acima.

### Exemplo de Requisição
```
curl -X POST http://localhost:5000/create_tag \
-H "Content-Type: application/json" \
-d '{"product_code": "1234567890"}'
```
### Exemplo de Resposta
```
{
  "data": {
    "type": "Imagem da Tag",
    "count": 1,
    "path": "caminho/para/barcode_1234567890.png"
  }
}
```
