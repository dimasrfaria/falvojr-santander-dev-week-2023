# Pipeline ETL: Marketing Bancário com IA Generativa 🚀

Este projeto é uma implementação prática do fluxo **ETL (Extract, Transform, Load)**, desenvolvido originalmente para o desafio **Santander Dev Week**. A solução foi adaptada para superar a descontinuidade da API original, utilizando manipulação de arquivos locais e integração com as tecnologias de IA de 2026.


## 📋 Resumo do Projeto

O objetivo principal é transformar dados brutos de clientes em mensagens de marketing personalizadas. O foco está na **Hyper-personalization**, garantindo que cada cliente receba uma comunicação única baseada em seu perfil, mantendo o *compliance* bancário.

---

## 🏗️ Arquitetura do Pipeline

### 1. FASE "E" -> EXTRACT (Extração)
Os dados são extraídos de um arquivo estruturado `SDW2026.csv` utilizando a biblioteca **Pandas**. 
* **Limitação de Amostragem**: Devido às cotas das APIs gratuitas, o processo é validado com um conjunto controlado de usuários.

### 2. FASE "T" -> TRANSFORMATION (Transformação)
Esta é a etapa de maior valor agregado, onde a inteligência artificial processa os dados:
* **Multi-LLM Support**: Integração com **OpenAI (GPT-3.5-Turbo)** e **Google Gemini (2.0 Flash)**.
* **Prompt Engineering**: Definição de diretrizes rígidas para manter o tom institucional e evitar a invenção de taxas ou valores.
* **Resiliência**: Implementação de pausas controladas (`time.sleep`) para evitar erros de limite de requisição (Rate Limit).

### 3. FASE "L" -> LOAD (Carregamento)
O resultado final é persistido localmente para manter o histórico das campanhas:
* **Persistência em CSV**: Gravação no arquivo `SDW2026_news.csv`.
* **Modo Append**: O sistema adiciona novas interações sem sobrescrever dados históricos.
* **Auditoria**: Registro automático de *Timestamp* para cada mensagem gerada.

---

## 🛠️ Tecnologias e Bibliotecas
* **Python 3.12+**
* **Pandas**: Processamento de tabelas e arquivos.
* **Google GenAI (SDK 2026)**: Motor de inteligência artificial.
* **Python-dotenv**: Gestão de variáveis de ambiente.
* **Google Colab Secrets**: Armazenamento seguro de credenciais.

---

## 🛡️ Segurança e Práticas Recomendadas
Para garantir a proteção das chaves de API e a qualidade do código, foram aplicadas as seguintes práticas:
* **Uso de `.gitignore`**: Arquivos sensíveis como `.env` e caches de sistema são ignorados pelo controle de versão.
* **Gestão de Segredos**: Uso de variáveis de ambiente para nunca expor chaves privadas no código fonte.
* **Tratamento de Exceções**: Blocos `try-except` robustos para garantir que falhas em um registro não interrompam todo o pipeline.

---

## 🚀 Como Executar
1. Certifique-se de ter as bibliotecas instaladas:
   ```bash
   pip install pandas google-genai python-dotenv
   
