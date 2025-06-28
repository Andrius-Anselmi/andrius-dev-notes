# 🧠 SQL Essencial para Programadores

Scripts organizados por categoria com **explicações linha a linha**. Ideal para consulta rápida no dia a dia.

---

## 📌 Índice

1. [📂 Criação de Tabelas](#criação-de-tabelas)
2. [📝 Inserção de Dados (](#inserção-de-dados)[`INSERT`](#inserção-de-dados)[)](#inserção-de-dados)
3. [🔍 Consultas (](#consultas)[`SELECT`](#consultas)[)](#consultas)
4. [✏️ Atualização (](#atualização)[`UPDATE`](#atualização)[)](#atualização)
5. [❌ Exclusão (](#exclusão)[`DELETE`](#exclusão)[)](#exclusão)
6. [🔗 Relacionamentos e Constraints (](#relacionamentos-e-constraints)[`FOREIGN KEY`](#relacionamentos-e-constraints)[)](#relacionamentos-e-constraints)
7. [📊 Funções de Agregação](#funções-de-agregação)
8. [📌 Views e Índices](#views-e-índices)
9. [🧩 Procedures Básicas (MySQL)](#procedures-básicas)
10. [💣 Truncate vs Delete](#truncate-vs-delete)
11. [🔁 Subqueries](#subqueries)
12. [💾 Backup e Restore](#backup-e-restore)

---

## 📂 Criação de Tabelas

```sql
-- Cria a tabela de usuários
CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY, -- chave primária autoincremental
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE, -- email deve ser único
    criado_em TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## 📝 Inserção de Dados

```sql
-- Inserindo um usuário
INSERT INTO usuarios (nome, email) VALUES ('Andrius Anselmi', 'andrius@email.com');
```

---

## 🔍 Consultas

```sql
-- Seleciona todos os usuários
SELECT * FROM usuarios;

-- Busca por nome específico
SELECT nome FROM usuarios WHERE nome LIKE 'Andrius%';

-- Ordenação decrescente por ID
SELECT * FROM usuarios ORDER BY id DESC;

-- Limitando resultados
SELECT * FROM usuarios LIMIT 10;
```

---

## ✏️ Atualização

```sql
-- Atualiza o e-mail de um usuário
UPDATE usuarios
SET email = 'novoemail@email.com'
WHERE id = 1;
```

---

## ❌ Exclusão

```sql
-- Remove um usuário pelo ID
DELETE FROM usuarios WHERE id = 1;
```

---

## 🔗 Relacionamentos e Constraints

```sql
-- Tabela cargos
CREATE TABLE cargos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL
);

-- Tabela funcionários com FK para cargos
CREATE TABLE funcionarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    cargo_id INT,
    FOREIGN KEY (cargo_id) REFERENCES cargos(id) -- FK simples
);
```

## ❌ Manipulação de Constraints

```sql
-- Remove a constraint de chave estrangeira antiga
ALTER TABLE Music DROP CONSTRAINT music_artist_fkey;

-- Corrige o nome da coluna (renomeia de 'artist' para 'artist_id')
ALTER TABLE Music RENAME COLUMN artist TO artist_id;

-- Adiciona novamente a constraint de chave estrangeira com o nome correto da coluna
ALTER TABLE Music
ADD CONSTRAINT fk_artist_music FOREIGN KEY (artist_id) REFERENCES Artist(id);
```

---

### 🎯 Manipulação de Constraints

| Ação                      | Script                                                                                           |
| ------------------------- | ------------------------------------------------------------------------------------------------ |
| ➕ Adicionar FK após criar | `ALTER TABLE funcionarios ADD CONSTRAINT fk_cargo FOREIGN KEY (cargo_id) REFERENCES cargos(id);` |
| ❌ Remover FK              | `ALTER TABLE funcionarios DROP FOREIGN KEY fk_cargo;`                                            |
| ✏️ Renomear FK (2 passos) | `DROP FOREIGN KEY` + `ADD CONSTRAINT novo_nome ...`                                              |

---

## 📊 Funções de Agregação

```sql
-- Total de usuários
SELECT COUNT(*) FROM usuarios;

-- Total por domínio de e-mail
SELECT SUBSTRING_INDEX(email, '@', -1) AS dominio, COUNT(*) AS total
FROM usuarios
GROUP BY dominio;
```

---

## 📌 Views e Índices

```sql
-- View de funcionários com nome do cargo
CREATE VIEW v_funcionarios AS
SELECT f.nome AS funcionario, c.nome AS cargo
FROM funcionarios f
JOIN cargos c ON f.cargo_id = c.id;

-- Índice no campo email
CREATE INDEX idx_email ON usuarios(email);
```

---

## 🧩 Procedure Básica

```sql
-- Cria uma procedure para buscar por domínio de e-mail
DELIMITER //
CREATE PROCEDURE buscarPorDominio(IN dominio_email VARCHAR(50))
BEGIN
    SELECT * FROM usuarios WHERE email LIKE CONCAT('%@', dominio_email);
END //
DELIMITER ;
```

---

## 💣 Truncate vs Delete

```sql
-- Remove todos os dados da tabela (sem log)
TRUNCATE TABLE usuarios;

-- Também remove, mas registra no log
DELETE FROM usuarios;
```

---

## 🔁 Subqueries

```sql
-- Buscar cargos com mais de 3 funcionários
SELECT nome FROM cargos
WHERE id IN (
    SELECT cargo_id FROM funcionarios
    GROUP BY cargo_id
    HAVING COUNT(*) > 3
);
```

---

## 💾 Backup e Restore

```bash
# Backup do banco
mysqldump -u root -p nome_do_banco > backup.sql

# Restauração
mysql -u root -p nome_do_banco < backup.sql
```

---

📌 *Use, modifique e contribua para deixar esse guia ainda melhor!*

