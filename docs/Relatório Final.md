# Projeto Banco de Dados Novemp


**Rafael Cabral Campos** 

**Filipe Simtob**

**Laura Neves**

**Anderson Babetto**

---

Professores:

**Prof. Marco Paulo Soares Gomes**

---

_Curso de Ciência de Dados, Unidade Praça da Liberdade_

_Instituto de Informática e Ciências Exatas – Pontifícia Universidade de Minas Gerais (PUC MINAS), Belo Horizonte – MG – Brasil_

---

## Resumo 

O projeto consistiu na criação de um banco de dados relacional para a empresa fictícia Novemp, com foco no setor de vendas. A estrutura foi pensada para armazenar e organizar dados de clientes, representantes, produtos, pedidos e pagamentos, garantindo integridade referencial e flexibilidade para análise. Foram elaborados modelos conceitual, lógico e físico, utilizando o MySQL como SGBD. Além disso, implementamos consultas SQL para responder a perguntas estratégicas do negócio, como identificação dos produtos mais vendidos, desempenho dos representantes e análise de compras por estado. O sistema final entrega uma base sólida e útil para apoiar a tomada de decisões comerciais baseadas em dados.

---

## Introdução

Neste projeto, desenvolvemos um banco de dados relacional para a empresa fictícia de elétrica Novemp, com foco no setor de vendas. A iniciativa teve como objetivo organizar e estruturar os dados comerciais da empresa, permitindo uma gestão mais eficiente e analítica. A partir de dados simulados, construímos modelos conceitual, lógico e físico, respeitando princípios de integridade e normalização. Também implementamos consultas SQL para gerar insights sobre clientes, produtos e representantes. O resultado é uma solução robusta, capaz de apoiar decisões estratégicas com base em dados reais.

---

###    Contextualização

Atualmente, a gestão de dados é um dos principais pilares para a eficiência e competitividade das empresas, especialmente em setores com grande volume de transações, como o setor elétrico. Segundo pesquisa da McKinsey & Company (2023), organizações orientadas por dados têm 23 vezes mais chances de conquistar clientes e 19 vezes mais probabilidade de serem lucrativas. Nesse cenário, bancos de dados bem estruturados se tornam ferramentas indispensáveis para armazenar, organizar e analisar informações de forma eficaz.

O presente trabalho insere-se na área de banco de dados e ciência de dados aplicada à gestão empresarial, com foco em processos comerciais. A proposta foi desenvolver um sistema de banco de dados relacional para a empresa fictícia de elétrica Novemp, com base em dados simulados e estruturados. O projeto teve como objetivo não apenas organizar o fluxo de informações, mas também permitir análises estratégicas que apoiem a tomada de decisões no setor de vendas da empresa.


---

###    Objetivo geral

Desenvolver um banco de dados relacional para atender às necessidades do setor de vendas de uma grande empresa do ramo elétrico, a Novemp. O objetivo principal foi estruturar as informações comerciais da empresa de forma organizada, segura e acessível, permitindo maior controle sobre pedidos, clientes, representantes e produtos. Através do projeto, buscou-se otimizar os processos internos da empresa e viabilizar análises estratégicas, contribuindo para uma gestão mais eficiente e orientada por dados.

---

### Tabela 1: Elementos do modelo conceitual do banco de dados Novemp (v1.0)

| Tipo            | Subtipo      | ID    | Rótulo                   | Referência                       |
|-----------------|--------------|-------|---------------------------|----------------------------------|
| Entidade        | Forte        | E001  | Cliente                  |                                  |
| Entidade        | Forte        | E002  | Representante            |                                  |
| Entidade        | Forte        | E003  | Parcela                  |                                  |
| Entidade        | Forte        | E004  | Produto                  |                                  |
| Entidade        | Forte        | E005  | Pedido                   |                                  |
| Entidade        | Associativa  | E006  | Itens                    |                                  |
| Entidade        | Fraca        | E007  | Telefone                 | E001                             |
| Entidade        | Fraca        | E008  | EnderecoPag              | E001                             |
| Entidade        | Fraca        | E009  | EnderecoEnt              | E001                             |
| Relacionamento  | Simples      | R001  | Possui                   | E004, E006                       |
| Relacionamento  | Simples      | R002  | Faz                      | E001, E005                       |
| Relacionamento  | Simples      | R003  | Realiza                  | E002, E005                       |
| Relacionamento  | Simples      | R004  | Possui                   | E005, E003                       |
| Relacionamento  | Simples      | R005  | Possui                   | E001, E007                       |
| Relacionamento  | Simples      | R006  | Possui                   | E001, E008                       |
| Relacionamento  | Simples      | R007  | Possui                   | E001, E009                       |
| Atributo        | Identificador| A001  | ID_Cliente               | E001                             |
| Atributo        | Simples      | A002  | Nome                     | E001                             |
| Atributo        | Simples      | A003  | CNPJ                     | E001                             |
| Atributo        | Simples      | A004  | Inscrição Estadual       | E001                             |
| Atributo        | Simples      | A005  | Razão Social             | E001                             |
| Atributo        | Simples      | A006  | Email                    | E001                             |
| Atributo        | Simples      | A007  | ID_EnderecoPag           | E008                             |
| Atributo        | Simples      | A008  | Logradouro               | E008, E009                       |
| Atributo        | Simples      | A009  | Número                   | E008, E009                       |
| Atributo        | Simples      | A010  | Complemento              | E008, E009                       |
| Atributo        | Simples      | A011  | Bairro                   | E008, E009                       |
| Atributo        | Simples      | A012  | Cidade                   | E008, E009                       |
| Atributo        | Simples      | A013  | Estado                   | E008, E009                       |
| Atributo        | Simples      | A014  | ID_EnderecoEnt           | E009                             |
| Atributo        | Simples      | A015  | ID_Telefone              | E007                             |
| Atributo        | Simples      | A016  | DDD                      | E007                             |
| Atributo        | Simples      | A017  | Número                   | E007                             |
| Atributo        | Simples      | A018  | Tipo                     | E007                             |
| Atributo        | Identificador| A019  | ID_Representante         | E002                             |
| Atributo        | Simples      | A020  | Nome                     | E002                             |
| Atributo        | Identificador| A021  | ID_Produto               | E004                             |
| Atributo        | Simples      | A022  | Nome                     | E004                             |
| Atributo        | Simples      | A023  | Valor                    | E004                             |
| Atributo        | Identificador| A024  | ID_Pedido                | E005                             |
| Atributo        | Simples      | A025  | Comissão                 | E005                             |
| Atributo        | Simples      | A026  | PrazoEntrega             | E005                             |
| Atributo        | Simples      | A027  | Frete                    | E005                             |
| Atributo        | Simples      | A028  | Data                     | E005                             |
| Atributo        | Simples      | A029  | Valor                    | E005                             |
| Atributo        | Simples      | A030  | QuantidadeParcelas       | E005                             |
| Atributo        | Identificador| A031  | ID_Parcela               | E003                             |
| Atributo        | Simples      | A032  | FormaPagamento           | E003                             |
| Atributo        | Simples      | A033  | Valor                    | E003                             |
| Atributo        | Simples      | A034  | DataPagamento            | E003                             |
| Atributo        | Simples      | A035  | DataVencimento           | E003                             |
| Atributo        | Identificador| A036  | ID_Itens                 | E006                             |
| Atributo        | Simples      | A037  | QuantidadeProdutos       | E006                             |
| Atributo        | Simples      | A038  | Quantidade               | R001    

---

## Indução de modelos

### Projeto Conceitual

Essa seção apresenta o projeto conceitual da Novemp (v1.0), descrevendo as principais estruturas e restrições conceituais do banco de dados. Particularmente, a Figura 1 apresenta o diagrama entidade-relacionamento (MER) do modelo conceitual da Novemp.
Além disso, a Tabela 1 fornece uma descrição mais detalhada dos elementos representados no diagrama da Figura 1. Nela, é possível observar que a descrição textual do minimundo identificou seis entidades e seus atributos. Também foram reconhecidos dois relacionamentos entre as entidades, juntamente com suas respectivas restrições de cardinalidade.



### Projeto Lógico

Nesta seção, exploramos o projeto lógico do banco de dados Novemp, destacando suas principais estruturas e restrições conforme o modelo relacional. A Figura 2 ilustra o diagrama relacional, construído a partir do modelo conceitual apresentado na Seção 3, traduzindo os elementos conceituais em uma representação lógica clara e estruturada.
A Figura 2 apresenta o diagrama relacional do banco de dados Novemp, no qual foram mapeadas dez entidades principais: Produtos, TiposProdutos, Clientes, Pedidos, Itens, Parcelas, Representantes, Telefones, EnderecoPagamento e EnderecoEntrega. O modelo contempla, em média, cinco atributos por entidade, refletindo um bom nível de detalhamento para representar as operações do sistema. Além disso, é possível observar diversas restrições de integridade referencial, totalizando onze relacionamentos entre tabelas, que garantem a consistência dos dados. A utilização de chaves primárias (PK) e estrangeiras (FK) está bem definida, o que favorece tanto a integridade quanto a normalização do modelo.
Esse diagrama é especialmente útil para visualizar de forma clara e estruturada as relações entre os dados, independentemente do Sistema Gerenciador de Banco de Dados (SGBD) relacional que venha a ser utilizado na implementação. 
Além do modelo de dados, uma etapa essencial no projeto lógico é definir qual abordagem e qual solução de banco de dados será utilizada. No caso da Novemp, optamos por seguir a abordagem relacional, adotando o MySQL como sistema gerenciador. Essa escolha se dá pela robustez, ampla aceitação no mercado e compatibilidade com as necessidades da aplicação.

---

## 8. Conclusão

A construção do banco de dados da empresa fictícia Novemp representou uma experiência completa de modelagem, implementação e análise de dados aplicados ao contexto empresarial. A partir de informações simuladas, conseguimos representar com fidelidade os processos do setor de vendas, contemplando desde o cadastro de clientes até a emissão de pedidos e controle de pagamentos. O projeto reforçou a importância de um modelo bem estruturado, com integridade referencial e normalização adequada, garantindo confiabilidade e consistência nas operações. A escolha pelo MySQL como SGBD se mostrou acertada, atendendo às necessidades técnicas com eficiência. Além disso, a elaboração de consultas SQL complexas permitiu extrair insights relevantes, como padrões de compra, desempenho de representantes e preferências por produto e região. As análises oferecidas podem servir de base para decisões mais estratégicas e direcionadas. O contato com a empresa também foi essencial para validar o sistema frente às demandas reais do mercado. Por fim, este trabalho evidencia o potencial dos bancos de dados como ferramentas não só operacionais, mas também analíticas e decisórias.







