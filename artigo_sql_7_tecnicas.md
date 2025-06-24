
# 7 Técnicas de SQL que Todo Desenvolvedor Precisa Dominar

## 🚀 Introdução

SQL (Structured Query Language) é uma das linguagens mais fundamentais para qualquer profissional que lida com dados. Seja você um desenvolvedor backend, analista de dados ou cientista de dados, o domínio de SQL é essencial para acessar, manipular e analisar informações em bancos de dados relacionais.

Apesar de parecer simples à primeira vista, SQL possui profundidade suficiente para permitir desde consultas básicas até operações complexas com alta performance. Neste artigo, você vai conhecer **7 técnicas essenciais de SQL** que todo desenvolvedor deveria dominar para se destacar no mercado de trabalho.

---

## 🔧 Técnica 1: JOINs (INNER, LEFT, RIGHT)

Os JOINs são utilizados para combinar dados de duas ou mais tabelas com base em uma condição comum — geralmente uma chave primária e uma chave estrangeira. Eles são fundamentais para trabalhar com bancos de dados relacionais.

### 📘 Exemplos:

#### 🔹 INNER JOIN
```sql
SELECT p.nome, o.valor
FROM pessoa p
INNER JOIN ordem o ON p.id = o.pessoa_id;
```

#### 🔹 LEFT JOIN
```sql
SELECT p.nome, o.valor
FROM pessoa p
LEFT JOIN ordem o ON p.id = o.pessoa_id;
```

#### 🔹 RIGHT JOIN
```sql
SELECT p.nome, o.valor
FROM pessoa p
RIGHT JOIN ordem o ON p.id = o.pessoa_id;
```

---

## 🔍 Técnica 2: Subqueries (Subconsultas)

As subqueries são instruções SQL aninhadas dentro de outras. Elas permitem isolar cálculos, filtrar dados com base em resultados intermediários e tornar a lógica das consultas mais modular e clara.

### 📘 Exemplos:

#### 🔹 Subquery no WHERE
```sql
SELECT nome
FROM cliente
WHERE id IN (
    SELECT cliente_id
    FROM pedido
);
```

#### 🔹 Subquery no SELECT
```sql
SELECT 
    c.nome,
    (SELECT SUM(valor) 
     FROM pedido p 
     WHERE p.cliente_id = c.id) AS total_pedidos
FROM cliente c;
```

#### 🔹 Subquery no FROM
```sql
SELECT media_por_produto.produto_id, AVG(media_por_produto.valor) AS media
FROM (
    SELECT produto_id, valor
    FROM pedido_item
) media_por_produto
GROUP BY media_por_produto.produto_id;
```

---

## 📊 Técnica 3: Funções de Agregação (SUM, COUNT, AVG...)

As funções de agregação são utilizadas para realizar cálculos sobre um conjunto de linhas e retornar um único valor resumido.

### 📘 Exemplos:

```sql
SELECT 
    TO_CHAR(data_pedido, 'MM/YYYY') AS mes,
    SUM(valor_total) AS total_vendas
FROM pedido
GROUP BY TO_CHAR(data_pedido, 'MM/YYYY');
```

```sql
SELECT COUNT(*) AS total_clientes
FROM cliente
WHERE status = 'Ativo';
```

```sql
SELECT cliente_id, AVG(valor_total) AS media_gastos
FROM pedido
GROUP BY cliente_id;
```

---

## 🪟 Técnica 4: Window Functions (ROW_NUMBER, RANK, etc.)

Permitem cálculos sobre um conjunto de linhas relacionadas à linha atual, sem colapsar os dados.

### 📘 Exemplos:

```sql
SELECT 
    cliente_id,
    id_pedido,
    ROW_NUMBER() OVER (PARTITION BY cliente_id ORDER BY data_pedido) AS numero_pedido
FROM pedido;
```

```sql
SELECT 
    cliente_id,
    SUM(valor_total) AS total,
    RANK() OVER (ORDER BY SUM(valor_total) DESC) AS posicao
FROM pedido
GROUP BY cliente_id;
```

```sql
SELECT 
    id_pedido,
    valor_total,
    LAG(valor_total) OVER (ORDER BY data_pedido) AS valor_anterior
FROM pedido;
```

---

## 🧱 Técnica 5: Common Table Expressions (CTEs com WITH)

As CTEs permitem criar blocos temporários nomeados dentro da query.

### 📘 Exemplo:

```sql
WITH pedidos_2024 AS (
    SELECT * 
    FROM pedido
    WHERE EXTRACT(YEAR FROM data_pedido) = 2024
)
SELECT cliente_id, COUNT(*) AS qtd_pedidos
FROM pedidos_2024
GROUP BY cliente_id;
```

---

## ⚡ Técnica 6: Indexação e Performance

Índices funcionam como atalhos para acelerar buscas no banco de dados.

### 📘 Exemplo de índice:

```sql
CREATE INDEX idx_cliente_cpf ON cliente(cpf);
```

---

## 🧠 Técnica 7: Stored Procedures e Views

### Stored Procedure:

```sql
CREATE OR REPLACE PROCEDURE atualiza_preco_produto (
    p_id_produto IN NUMBER,
    p_novo_preco IN NUMBER
) AS
BEGIN
    UPDATE produto
    SET preco = p_novo_preco
    WHERE id = p_id_produto;
END;
```

### View:

```sql
CREATE VIEW vw_clientes_ativos AS
SELECT id, nome, email
FROM cliente
WHERE status = 'Ativo';
```

---

## ✅ Conclusão (Técnica 3R)

### 🧠 Reforce  
Dominar SQL não é um diferencial — é uma **necessidade** para qualquer desenvolvedor ou analista que deseja trabalhar com dados de forma eficiente. As técnicas que vimos aqui — JOINs, subqueries, funções de agregação, CTEs, window functions e mais — são **habilidades essenciais** para escrever consultas rápidas, organizadas e poderosas.

### 🧩 Relembre  
Você aprendeu neste artigo:
- Como usar JOINs de forma estratégica  
- A força das subqueries e CTEs para modularização  
- Como funções de agregação e janelas entregam análises ricas  
- A importância de índices e boas práticas para performance  
- E como procedures e views ajudam na manutenção e reutilização

### 🚀 Reaja  
Agora é a sua vez:  
Qual dessas técnicas você **já usa**? Qual você **vai começar a praticar hoje mesmo**?

👉 Deixe seu comentário aqui embaixo, compartilhe com sua rede e **marque aquele amigo ou colega que também precisa dominar SQL**.  
Vamos juntos construir soluções mais inteligentes e performáticas com SQL!
