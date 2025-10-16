# Processador de Chunks - Text & PDF Chunking Tool

[![Python](https://img.shields.io/badge/Python-3.7+-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Uma ferramenta robusta para dividir textos longos e documentos PDF em chunks menores, otimizada para processamento por sistemas de IA e RAG (Retrieval-Augmented Generation).

## ✨ Características

- **Chunking baseado em tokens**: Usa tokenizers do Hugging Face para controle preciso de tamanho
- **Suporte a PDF**: Extração automática de texto de arquivos PDF
- **Sobreposição configurável**: Mantém contexto entre chunks consecutivos
- **Tratamento de erros**: Logging detalhado e validações robustas
- **Flexibilidade**: Parâmetros totalmente configuráveis
- **Performance**: Processamento eficiente para textos grandes

## 🚀 Instalação

### Pré-requisitos
- Python 3.7 ou superior
- Conta no Hugging Face (para download de modelos)

### Instalação das dependências

```bash
# Instalar dependências principais
pip install transformers torch

# Para suporte a PDF (opcional, mas recomendado)
pip install pdfplumber

# Para desenvolvimento (opcional)
pip install pytest black flake8
```

## 📖 Uso

### Chunking Básico de Texto

```python
from extraction import simple_text_chunker

# Texto de exemplo
texto = """
Seu texto longo aqui. A ferramenta irá dividir automaticamente
em chunks menores baseados no número de tokens.
"""

# Criar chunks
chunks = simple_text_chunker(
    text=texto,
    max_tokens=300,      # Máximo de tokens por chunk
    overlap=20          # Sobreposição entre chunks
)

# Cada chunk contém metadados detalhados
for chunk in chunks:
    print(f"Tokens: {chunk['tokens']}")
    print(f"Texto: {chunk['text'][:100]}...")
```

### Processamento de PDF

```python
from extraction import chunk_pdf

# Processar PDF completo
chunks = chunk_pdf(
    pdf_path="documento.pdf",
    max_tokens=512,
    overlap=50
)

print(f"PDF dividido em {len(chunks)} chunks")
```

### Exemplo Completo

```python
# Executar o arquivo principal para ver demonstração
python extraction.py
```

## 🔧 API

### `simple_text_chunker(text, embed_model, max_tokens, overlap)`

Divide texto em chunks baseados em tokens.

**Parâmetros:**
- `text` (str): Texto a ser dividido
- `embed_model` (str): Modelo do tokenizer (padrão: "sentence-transformers/all-MiniLM-L6-v2")
- `max_tokens` (int): Máximo de tokens por chunk (padrão: 300)
- `overlap` (int): Tokens de sobreposição (padrão: 20)

**Retorno:** Lista de dicionários com:
- `text`: Texto do chunk
- `tokens`: Número de tokens
- `start_token`/`end_token`: Posições dos tokens
- `start_char`/`end_char`: Posições de caracteres
- `chunk_id`: ID sequencial do chunk

### `extract_text_from_pdf(pdf_path)`

Extrai texto de um arquivo PDF.

**Parâmetros:**
- `pdf_path` (str): Caminho para o arquivo PDF

**Retorno:** String com texto extraído

### `chunk_pdf(pdf_path, embed_model, max_tokens, overlap)`

Processa PDF completo: extrai texto e divide em chunks.

**Parâmetros:** Combinados dos métodos acima

**Retorno:** Lista de chunks (mesmo formato de `simple_text_chunker`)

## ⚙️ Configuração

### Modelos de Tokenizer

A ferramenta suporta qualquer modelo do Hugging Face:

```python
# Modelo multilíngue
chunks = simple_text_chunker(text, embed_model="bert-base-multilingual-cased")

# Modelo específico para português
chunks = simple_text_chunker(text, embed_model="neuralmind/bert-base-portuguese-cased")
```

### Otimização de Performance

Para textos muito grandes:
- Ajuste `max_tokens` conforme limite do seu modelo de IA
- Use sobreposição menor para reduzir redundância
- Considere processamento em lotes para PDFs grandes

## 🧪 Testes

```bash
# Executar testes
pytest

# Verificar qualidade do código
flake8 extraction.py
black extraction.py
```

## 📋 Limitações

- PDFs com imagens ou tabelas complexas podem ter extração de texto limitada
- Desempenho depende da velocidade de download do modelo tokenizer
- Memória limitada para textos extremamente grandes (>100MB)

## 🤝 Contribuição

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo `LICENSE` para detalhes.

## 🙏 Agradecimentos

- [Hugging Face Transformers](https://huggingface.co/docs/transformers/index) - Para tokenization
- [pdfplumber](https://github.com/jsvine/pdfplumber) - Para extração de PDF
- [Sentence Transformers](https://www.sbert.net/) - Para modelos de embedding

## 📞 Suporte

Para dúvidas ou sugestões:
- Abra uma issue no GitHub
- Email: lucianomevam@outlook.com
