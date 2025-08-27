# Tipos de Dados em Bancos de Dados

Neste conteúdo, você vai aprender sobre a importância dos **tipos de dados** em bancos de dados e como eles impactam o armazenamento e a eficiência das aplicações.  

Descubra os diferentes tipos, como **INTEGER, TEXT, REAL e BLOB**, e como escolher o correto para garantir a integridade e o desempenho dos seus sistemas.

---

## O que são Tipos de Dados?

Cada dado armazenado em um banco de dados contém um tipo, como **inteiro, texto, ponto flutuante, nulo, binário**, entre outros.  

⚠️ Importante: os tipos suportados pelos bancos de dados **não são padronizados**. É sempre necessário verificar a documentação do SGBD utilizado para saber quais tipos são disponibilizados.

---

## Tipos de Dados no SQLite

O **SQLite** trata os dados de forma diferente de outros bancos.  
Enquanto em outros SGBDs temos um número limitado de tipos, no SQLite cada valor armazenado pertence a uma das seguintes classes:

- **NULL** → Para valores nulos.  
- **INTEGER** → Valores inteiros.  
- **REAL** → Valores numéricos com ponto flutuante.  
- **TEXT** → Sequências de texto.  
- **BLOB** → Dados binários (imagens, arquivos, etc.).

---

## Afinidades de Tipo no SQLite

Apesar de parecer um número limitado de classes, o SQLite suporta o conceito de **afinidades de tipo** para as colunas.  

➡️ Isso significa que, ao criar uma tabela, não é necessário definir um tipo estático para uma coluna.  
Em vez disso, definimos a **afinidade** dela, permitindo armazenar diferentes tipos de dados em uma mesma coluna.

As afinidades disponíveis no SQLite são:

- **TEXT**
- **NUMERIC**
- **INTEGER**
- **REAL**
- **NONE** (sem preferência de armazenamento, não ocorre conversão de valores)

---

## Mapeamento de Tipos para Afinidades

O SQLite consegue **mapear tipos não suportados** para os tipos conhecidos utilizando afinidades.  

Exemplo:  
O tipo **VARCHAR(n)**, comum no MySQL e PostgreSQL, é convertido para **TEXT** no SQLite.  

Isso nos permite definir atributos em `CREATE TABLE` com tipos usados em produção, mesmo que não sejam nativos do SQLite.

---

## Tabela de Afinidades do SQLite

| Tipo no CREATE TABLE                                                                 | Afinidade |
|--------------------------------------------------------------------------------------|-----------|
| INT, INTEGER, TINYINT, SMALLINT, MEDIUMINT, BIGINT, UNSIGNED BIG INT, INT2, INT8     | INTEGER   |
| CHARACTER(20), VARCHAR(255), VARYING CHARACTER(255), NCHAR(55), NATIVE CHARACTER(70), NVARCHAR(100), TEXT, CLOB | TEXT |
| BLOB                                                                                 | BLOB      |
| REAL, DOUBLE, DOUBLE PRECISION, FLOAT                                                | REAL      |
| NUMERIC, DECIMAL(10,5), BOOLEAN, DATE, DATETIME                                      | NUMERIC   |

📌 Essa tabela mostra como o SQLite converte automaticamente tipos declarados em colunas para uma afinidade suportada.

---

## Conclusão

Mesmo utilizando o SQLite em ambiente de desenvolvimento, podemos definir os atributos das tabelas com os tipos que utilizaremos em produção.  
Graças ao sistema de **afinidades**, o SQLite garante compatibilidade e flexibilidade no armazenamento dos dados.

---
