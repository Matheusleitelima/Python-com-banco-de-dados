# 🔌 Conectores para Banco de Dados em Python

Este documento apresenta os principais **conectores de banco de dados em
Python**, essenciais para desenvolvedores que buscam integrar suas
aplicações com diferentes sistemas de gerenciamento de bancos de dados
(SGBDs).

------------------------------------------------------------------------

## 📌 O que são conectores?

Conectores (ou adaptadores) são **bibliotecas** que permitem a
comunicação entre uma aplicação Python e um banco de dados.\
Eles seguem a especificação **PEP 249 - Python Database API (DB-API
2.0)**, que garante uma interface padronizada e consistente.

------------------------------------------------------------------------

## 🛠️ Padrões da DB-API 2.0

-   **Nomes de métodos**: `close`, `commit`, `cursor`
-   **Nomes de classes**: `Connection`, `Cursor`
-   **Tipos de exceção**: `IntegrityError`, `InternalError`

------------------------------------------------------------------------

## 🚀 Principais Conectores

### PostgreSQL

-   `psycopg2` → Conector mais utilizado para PostgreSQL.

### MySQL

-   `mysqlclient`
-   `PyMySQL`
-   `mysql-connector-python`

### SQLite

-   `sqlite3` → Adaptador padrão do Python, já incluído na linguagem.

------------------------------------------------------------------------

## 📊 Tabela Comparativa

  Banco de Dados   Conectores Disponíveis
  ---------------- ---------------------------------------
  PostgreSQL       psycopg2
  MySQL            mysqlclient, PyMySQL, mysql-connector
  SQLite           sqlite3 (padrão do Python)

------------------------------------------------------------------------

## 🧩 Exemplo de Uso

### Exemplo com SQLite

``` python
import sqlite3

# Conectar ao banco (ou criar se não existir)
con = sqlite3.connect("meubanco.db")

# Criar cursor
cur = con.cursor()

# Criar tabela
cur.execute("CREATE TABLE IF NOT EXISTS usuarios (id INTEGER PRIMARY KEY, nome TEXT)")

# Inserir dados
cur.execute("INSERT INTO usuarios (nome) VALUES (?)", ("Matheus",))

# Confirmar transação
con.commit()

# Consultar dados
cur.execute("SELECT * FROM usuarios")
print(cur.fetchall())

# Fechar conexão
con.close()
```

------------------------------------------------------------------------

## 📚 Documentações Oficiais

-   [psycopg2](https://www.psycopg.org/)
-   [mysqlclient](https://mysqlclient.readthedocs.io/)
-   [PyMySQL](https://pymysql.readthedocs.io/)
-   [MySQL
    Connector/Python](https://dev.mysql.com/doc/connector-python/en/)
-   [sqlite3](https://docs.python.org/3/library/sqlite3.html)

------------------------------------------------------------------------

## ✨ Conclusão

A escolha do conector adequado pode impactar: - Performance ⚡ -
Facilidade de instalação 🔧 - Compatibilidade com recursos avançados do
banco de dados 🔗

Utilizar conectores compatíveis com a **PEP 249** garante portabilidade
e facilidade de manutenção no desenvolvimento de aplicações.

------------------------------------------------------------------------

## 👨‍💻 Autor

Desenvolvido por **Matheus** 🚀


# 🗄️ Principais Métodos e Exceções dos Conectores em Python

Para desenvolver aplicações robustas que interagem com bancos de dados,
é essencial conhecer os **métodos e exceções** oferecidos pelos
conectores que seguem a especificação **DB-API 2.0 (PEP 249)**.

Esses recursos permitem gerenciar conexões, executar operações e lidar
com erros de forma consistente entre diferentes SGBDs.

------------------------------------------------------------------------

## 📌 Principais Classes e Métodos

### 🔹 `connect`

-   Função global utilizada para criar uma conexão com o banco de dados.
-   Retorna um objeto da classe **Connection**.

### 🔹 `Connection`

Classe que gerencia as operações com o banco de dados.

**Métodos principais:** - `commit()` → confirma as operações
pendentes. - `rollback()` → desfaz as operações pendentes. - `cursor()`
→ retorna um objeto **Cursor**. - `close()` → encerra a conexão.

### 🔹 `Cursor`

Classe utilizada para enviar comandos ao banco de dados.

**Métodos principais:** - `execute(sql, params)` → executa comandos
SQL. - `fetchone()` → retorna a próxima linha de uma consulta. -
`fetchall()` → retorna todas as linhas de uma consulta.

------------------------------------------------------------------------

## 🔄 Fluxo de Trabalho Típico

1.  Conectar ao banco de dados (`connect`)
2.  Criar um cursor (`cursor`)
3.  Executar comandos (`execute`)
4.  Confirmar transações (`commit`)
5.  Fechar cursor e conexão (`close`)

------------------------------------------------------------------------

## 🧩 Exemplo com SQLite

``` python
import sqlite3 as conector

# Criar conexão
con = conector.connect("meubanco.db")

# Criar cursor
cur = con.cursor()

# Criar tabela
cur.execute("CREATE TABLE IF NOT EXISTS usuarios (id INTEGER PRIMARY KEY, nome TEXT)")

# Inserir dado
cur.execute("INSERT INTO usuarios (nome) VALUES (?)", ("Matheus",))

# Confirmar transação
con.commit()

# Consultar dados
cur.execute("SELECT * FROM usuarios")
print(cur.fetchall())

# Fechar conexão
con.close()
```

> 🔄 Para usar MySQL ou PostgreSQL, basta trocar o import para
> `import mysql.connector as conector` ou
> `import psycopg2 as conector`.\
> Graças à **DB-API 2.0**, a estrutura do código permanece a mesma!

------------------------------------------------------------------------

## ⚠️ Principais Exceções da DB-API 2.0

  ------------------------------------------------------------------------------
  Exceção               Descrição
  --------------------- --------------------------------------------------------
  `Error`               Classe base para todas as exceções.

  `DatabaseError`       Erros gerais relacionados ao banco de dados.

  `IntegrityError`      Violação de integridade (ex.: chave estrangeira, valores
                        únicos).

  `OperationalError`    Problemas operacionais fora do controle do programador
                        (ex.: desconexão).

  `ProgrammingError`    Erros de programação (ex.: SQL inválido, tabela
                        inexistente).

  `NotSupportedError`   Operações não suportadas pelo banco (ex.: rollback em DB
                        sem transações).
  ------------------------------------------------------------------------------

------------------------------------------------------------------------

## 🔎 Observações sobre SQLite

-   Disponível nativamente no **Python 3.7+** (módulo `sqlite3`).
-   Banco de dados completo, mas **não possui autenticação**
    (usuários/permissões).
-   Suporta:
    -   Subconsultas
    -   Transações
    -   Junções
    -   Índices, visões, gatilhos
    -   Full Text Search (FTS)
-   Não possui servidor → acesso remoto é limitado e pouco eficiente.

⚠️ Apesar de não ter autenticação nativa, é altamente recomendado
implementar **controle de acesso na aplicação**.

------------------------------------------------------------------------

## ✨ Conclusão

-   Os métodos `connect`, `commit`, `execute`, `fetch*` e `close` são
    comuns a todos os conectores.\
-   As exceções da DB-API 2.0 fornecem uma maneira consistente de tratar
    erros.\
-   O conhecimento desses padrões garante **portabilidade e robustez**
    no desenvolvimento de aplicações com banco de dados.

------------------------------------------------------------------------

## 👨‍💻 Autor

Desenvolvido por **Matheus** 🚀
