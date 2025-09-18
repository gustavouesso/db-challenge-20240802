# 📊 Desafio de Consultas SQL

Este projeto consiste em criar consultas SQL a partir de um modelo de dados fornecido.  
O objetivo é resolver os exercícios propostos pela plataforma **Coodesh**.

---

## 📌 Modelo de Dados
O banco de dados contém as seguintes entidades principais:
- **customers** (clientes)  
- **staffs** (funcionários)  
- **orders / order_items** (pedidos e itens)  
- **stores** (lojas)  
- **products / brands / categories** (produtos, marcas e categorias)  
- **stocks** (estoque de produtos por loja)  

---

## 📝 Consultas Solicitadas

### 1. Listar todos os Clientes que não tenham realizado uma compra
    ```sql
    SELECT c.customer_id, c.first_name, c.last_name
    FROM customers c
    LEFT JOIN orders o ON c.customer_id = o.customer_id
    WHERE o.order_id IS NULL;

2. Listar os Produtos que não tenham sido comprados
    SELECT p.product_id, p.product_name
    FROM products p
    LEFT JOIN order_items oi ON p.product_id = oi.product_id
    WHERE oi.order_id IS NULL;

3. Listar os Produtos sem Estoque
    SELECT p.product_id, p.product_name
    FROM products p
    LEFT JOIN stocks s ON p.product_id = s.product_id
    WHERE s.quantity IS NULL OR s.quantity = 0;

4. Apresentar a quantidade de vendas de uma determinada Marca por Loja
    SELECT b.brand_name,
        st.store_name,
        COUNT(oi.order_id) AS total_vendas
    FROM order_items oi
    JOIN products p ON oi.product_id = p.product_id
    JOIN brands b ON p.brand_id = b.brand_id
    JOIN orders o ON oi.order_id = o.order_id
    JOIN stores st ON o.store_id = st.store_id
    WHERE b.brand_name = 'Nike'
    GROUP BY b.brand_name, st.store_name;

5. Listar os Funcionários que não estejam relacionados a um Pedido
    SELECT s.staff_id, s.first_name, s.last_name
    FROM staffs s
    LEFT JOIN orders o ON s.staff_id = o.staff_id
    WHERE o.order_id IS NULL;

🚀 Como Executar
Importe o esquema do banco de dados no seu SGBD (PostgreSQL, MySQL, SQL Server, etc).

Abra o cliente SQL de sua preferência (DBeaver, pgAdmin, MySQL Workbench...).

Execute as queries acima diretamente no banco.

Substitua parâmetros como nome da marca quando necessário.

📂 Estrutura do Repositório
├── README.md   # Documentação do projeto
├── queries.sql # Arquivo opcional com todas as queries reunidas

🛠️ Tecnologias Utilizadas
    - SQL ANSI
    - SGBD compatível (PostgreSQL/MySQL/SQL Server)

📌 Observações
    - Este desafio foi proposto pela Coodesh.
    - Certifique-se de ajustar as queries conforme o SGBD que você utilizar (sintaxe pode variar).