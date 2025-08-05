# Consultas SQL

Cada uma dessas consultas foi proposta pelo professor para testar nossa base de dados em um SGBD. Foram elaboradas 10 perguntas relacionadas à base de dados e à linguagem de programação SQL. 
O primeiro parágrafo corresponde à pergunta elaborada pelo professor. O segundo parágrafo apresenta a pergunta que nós formulamos para tentar responder à questão inicial. Já o último parágrafo contém o código que resolve as perguntas.
Relembrando que as perguntas foram divididas pelos membros do grupo, cada um pegando algumas para fazer.

---

# Perguntas:

 *1)* 
Junção de 2 ou mais tabelas com GROUP BY, sem HAVING, usando uma função agregada qualquer (MIN, MAX, AVG, SUM, COUNT). Use ORDER BY;

Qual o valor total pago por cada cliente? Ordenado do maior para o menor.

SELECT c.Nome AS NomeCliente, SUM(p.Valor) AS TotalPago

FROM Pedidos p

JOIN Clientes c ON p.ID_Cliente = c.ID_Cliente

GROUP BY c.ID_Cliente

ORDER BY TotalPago DESC;

---

*2)*
Junção de 3 ou mais tabelas, usando os operadores IN/NOT IN e IS NULL/IS NOT NULL;

Quais pedidos contêm produtos da categoria ‘Quadro’ que já tiveram parcelas pagas?

SELECT p.ID_Pedidos, c.Nome AS NomeCliente, pr.Nome AS Produto, tp.Categoria, par.DataPagamento, par.valor AS ValorPago

FROM Pedidos p

JOIN Itens i ON p.ID_Pedidos = i.ID_Pedido

JOIN Produtos pr ON i.ID_Produto = pr.ID_Produtos

JOIN TiposProdutos tp ON pr.ID_Tipo = tp.ID_TiposProdutos

JOIN Parcelas par ON p.ID_Pedidos = par.ID_Pedido

JOIN Clientes c ON p.ID_Cliente = c.ID_Cliente

WHERE tp.Categoria IN ('Quadro')

AND par.DataPagamento IS NOT NULL

ORDER BY par.DataPagamento DESC;

---

*3)*
Subselect com correlação;

Quais clientes fizeram pedidos com valor acima da média dos pedidos que eles mesmos já realizaram?

SELECT c.ID_Cliente, p.ID_Pedidos, c.Nome, p.Valor,ROUND((SELECT AVG(p2.Valor)

FROM Pedidos p2

WHERE p2.ID_Cliente = p.ID_Cliente),2) AS MediaValor
    
FROM Clientes c

JOIN Pedidos p ON c.ID_Cliente = p.ID_Cliente

WHERE p.Valor > (

SELECT AVG(p2.Valor)
 
FROM Pedidos p2
 
WHERE p2.ID_Cliente = p.ID_Cliente);

---

*4)*
Junção de 3 ou mais tabelas, usando os operadores LIKE e BETWEEN;

Quais representantes tem clientes que compraram produtos do tipo cabine em 2024?

SELECT 

r.Nome AS NomeRepresentante,

c.Nome AS NomeCliente,

p.Data AS DataCompra,

p.ID_Pedidos AS IDPedido

FROM pedidos p

JOIN clientes c ON p.ID_Cliente = c.ID_Cliente

JOIN representantes r ON p.ID_Representante = r.ID_Representantes

JOIN itens i ON i.ID_Pedido = p.ID_Pedidos

JOIN produtos pr ON i.ID_Produto = pr.ID_Produtos

JOIN tiposprodutos tp ON pr.ID_Tipo = tp.ID_TiposProdutos

WHERE tp.Categoria  LIKE '%cabine%'

AND p.Data BETWEEN '2024-01-01' AND '2024-12-31';

---

*5)*
Subselect sem correlação;

Quais pedidos tem valor maior que o valor médio de todos os pedidos da empresa?

SELECT 
p.ID_Pedidos,

p.ID_Cliente,

c.Nome AS NomeCliente,

p.Valor,

NULL AS MediaGeral

FROM pedidos p

JOIN clientes c ON p.ID_Cliente = c.ID_Cliente

WHERE p.Valor > 

(SELECT AVG(Valor) FROM pedidos)

UNION ALL

SELECT 

NULL AS ID_Pedidos,

NULL AS ID_Cliente,

NULL AS NomeCliente,

NULL AS Valor,

ROUND(AVG(Valor), 2) AS MediaGeral

FROM pedidos

ORDER BY MediaGeral IS NULL, ID_Pedidos;
;

---

*6)*
Junção de 2 ou mais tabelas com GROUP BY e HAVING, usando uma função agregada qualquer (MIN, MAX, AVG, SUM, COUNT);

Quais clientes fizeram mais de 1 pedido? Liste o nome e a quantidade de pedidos de cada um.

SELECT c.Nome, COUNT(p.ID_Pedidos) AS QuantidadePedidos

FROM Clientes c

JOIN Pedidos p ON c.ID_Cliente = p.ID_Cliente

GROUP BY c.Nome

HAVING COUNT(p.ID_Pedidos) > 1;

---

*7)*
Subselect com EXISTS;

Liste os nomes dos representantes que já realizaram ao menos um contato com algum cliente.

SELECT r.Nome

FROM Representantes r

WHERE EXISTS (

SELECT 1

FROM Contatos c

WHERE c.ID_Representante = r.ID_Representantes

GROUP BY c.ID_Representante

HAVING COUNT(*) > 1);

---

*8)*
Junção de 2 ou mais tabelas com GROUP BY, HAVING e ALL;

Quais clientes fizeram pedidos cujo valor total foi maior do que todos os pedidos feitos por clientes do estado de São Paulo?

SELECT

c.Nome,

SUM(p.Valor) AS total_pedidos

FROM

Clientes c

JOIN

Pedidos p ON c.ID_Cliente = p.ID_Cliente   
GROUP BY

c.ID_Cliente, c.Nome

HAVING

SUM(p.Valor) > ALL (

SELECT

SUM(p2.Valor)

FROM

Clientes c2

JOIN

Pedidos p2 ON c2.ID_Cliente = p2.ID_Cliente

JOIN

EndereçoEntrega e2 ON c2.ID_Cliente = e2.ID_Cliente

WHERE

e2.Estado = 'São Paulo'

GROUP BY

p2.ID_Cliente);

---

*9)*
Junção de 3 ou mais tabelas, com ORDER BY;

Quais são todos os produtos que cada cliente comprou, o nome do cliente e o nome do produto? Ordene pelo nome do cliente.

SELECT  

c.Nome AS NomeCliente,

pr.Nome AS NomeProduto,

SUM(i.Quantidade) AS QuantidadeTotal

FROM 

Clientes c

JOIN 

Pedidos pe ON c.ID_Cliente = pe.ID_Cliente

JOIN 

Itens i ON pe.ID_Pedidos = i.ID_Pedido

JOIN 

Produtos pr ON i.ID_Produto = pr.ID_Produtos

GROUP BY 

c.Nome, pr.Nome

ORDER BY 

c.Nome ASC;

---

*10)*
Junção de 3 ou mais tabelas, com ORDER BY e filtros na cláusula WHERE;

Liste o nome dos clientes, o nome dos produtos que eles compraram e a data do pedido, mas só mostre pedidos feitos após '2025-01-01'. Ordene pela data do pedido, da mais recente para a mais antiga.

SELECT 

c.Nome AS NomeCliente,

pr.Nome AS NomeProduto,

pe.Data AS DataPedido

FROM 

Clientes c

JOIN 

Pedidos pe ON c.ID_Cliente = pe.ID_Cliente

JOIN 

Itens i ON pe.ID_Pedidos = i.ID_Pedido

JOIN 

Produtos pr ON i.ID_Produto = pr.ID_Produtos

WHERE 

pe.Data > '2025-01-01'

ORDER BY 

pe.Data DESC;

---



