# Exemplo de Modelo RAG

Uma implementação que aproveita a engenharia de prompt e a Geração Aumentada por Recuperação (RAG) para aprimorar o desempenho do LLM.

## Descrição

Este projeto demonstra uma abordagem RAG (Retrieval-Augmented Generation) que utiliza uma base de conhecimento estruturada em grafo. A inspiração para esta implementação vem de dois artigos de referência:

-   **Construindo RAGs com Grafos**[https://medium.com/luizalabs/construindo-rags-com-grafos-4bc6076f01a8]: Este artigo, do LuizaLabs, detalha como a estruturação do conhecimento em grafos pode otimizár a recuperação de informações relevantes, superando as limitações de abordagens tradicionais baseadas em "força bruta".
-   **O que é Geração Aumentada por Recuperação (RAG)?**[https://www.databricks.com/br/glossary/retrieval-augmented-generation-rag]: Uma visão geral da Databricks sobre a arquitetura RAG, que aumenta os modelos de linguagem com informações de fontes de conhecimento externas.

O RAG permite que os modelos de linguagem acessem e utilizem informações atualizadas e específicas do domínio, resultando em respostas mais precisas e contextualmente relevantes. Nossa implementação utiliza um grafo semântico para conectar documentos com base em sua similaridade, permitindo uma recuperação de contexto mais rica e eficiente.

## Como Funciona

O fluxo de trabalho do projeto é o seguinte:

1.  **Geração de Embeddings**: Os documentos de texto são convertidos em representações vetoriais (embeddings) usando o modelo `nomic-embed-text`.
2.  **Construção do Grafo**: Um grafo é construído onde cada documento é um nó. As arestas entre os nós são criadas com base na similaridade de cosseno entre seus embeddings.
3.  **Consulta RAG**: Quando uma consulta é feita, o sistema:
    * Gera o embedding da consulta.
    * Identifica os documentos mais relevantes (top-k) com base na similaridade.
    * Expande o contexto incluindo os vizinhos desses nós no grafo.
4.  **Geração de Resposta**: O contexto recuperado é então combinado com a consulta original em um prompt, que é enviado a um modelo de linguagem (neste caso, `llama3`) para gerar a resposta final.

## Licença

Este projeto está licenciado sob a Licença MIT. Consulte o arquivo [LICENSE](rag-model-example/LICENSE) para obter detalhes.