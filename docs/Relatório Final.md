# Projeto Banco de Dados Novemp


**Rafael Cabral** 

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

### Modelo 1: Algoritmo

Substitua o título pelo nome do algoritmo que será utilizado. P. ex. árvore de decisão, rede neural, SVM, etc.
Justifique a escolha do modelo.
Apresente o processo utilizado para amostragem de dados (particionamento, cross-validation).
Descreva os parâmetros utilizados. 
Apresente trechos do código utilizado comentados. Se utilizou alguma ferramenta gráfica, apresente imagens
com o fluxo de processamento.

### Modelo 2: Algoritmo

Repita os passos anteriores para o segundo modelo.


## Resultados

### Resultados obtidos com o modelo 1.

Apresente aqui os resultados obtidos com a indução do modelo 1. 
Apresente uma matriz de confusão quando pertinente. Apresente as medidas de performance
apropriadas para o seu problema. 
Por exemplo, no caso de classificação: precisão, revocação, F-measure, acurácia.

### Interpretação do modelo 1

Apresente os parâmetros do modelo obtido. Tentre mostrar as regras que são utilizadas no
processo de 'raciocínio' (*reasoning*) do sistema inteligente. Utilize medidas como 
o *feature importances* para tentar entender quais atributos o modelo se baseia no
processo de tomada de decisão.


### Resultados obtidos com o modelo 2.

Repita o passo anterior com os resultados do modelo 2.

### Interpretação do modelo 2

Repita o passo anterior com os parâmetros do modelo 2.


## Análise comparativa dos modelos

Discuta sobre as forças e fragilidades de cada modelo. Exemplifique casos em que um
modelo se sairia melhor que o outro. Nesta seção é possível utilizar a sua imaginação
e extrapolar um pouco o que os dados sugerem.


### Distribuição do modelo (opcional)

Tende criar um pacote de distribuição para o modelo construído, para ser aplicado 
em um sistema inteligente.


## 8. Conclusão

Apresente aqui a conclusão do seu trabalho. Discussão dos resultados obtidos no trabalho, 
onde se verifica as observações pessoais de cada aluno.

Uma conclusão deve ter 3 partes:

   * Breve resumo do que foi desenvolvido
	 * Apresenação geral dos resultados obtidos com discussão das vantagens e desvantagens do sistema inteligente
	 * Limitações e possibilidades de melhoria


# REFERÊNCIAS

Como um projeto de sistema inteligente não requer revisão bibliográfica, 
a inclusão das referências não é obrigatória. No entanto, caso você 
tenha utilizado referências na introdução ou deseje 
incluir referências relacionadas às tecnologias, padrões, ou metodologias 
que serão usadas no seu trabalho, relacione-as de acordo com a ABNT.

Verifique no link abaixo como devem ser as referências no padrão ABNT:

http://www.pucminas.br/imagedb/documento/DOC\_DSC\_NOME\_ARQUI20160217102425.pdf

Por exemplo:

**[1]** - _ELMASRI, Ramez; NAVATHE, Sham. **Sistemas de banco de dados**. 7. ed. São Paulo: Pearson, c2019. E-book. ISBN 9788543025001._

**[2]** - _COPPIN, Ben. **Inteligência artificial**. Rio de Janeiro, RJ: LTC, c2010. E-book. ISBN 978-85-216-2936-8._

**[3]** - _CORMEN, Thomas H. et al. **Algoritmos: teoria e prática**. Rio de Janeiro, RJ: Elsevier, Campus, c2012. xvi, 926 p. ISBN 9788535236996._

**[4]** - _SUTHERLAND, Jeffrey Victor. **Scrum: a arte de fazer o dobro do trabalho na metade do tempo**. 2. ed. rev. São Paulo, SP: Leya, 2016. 236, [4] p. ISBN 9788544104514._

**[5]** - _RUSSELL, Stuart J.; NORVIG, Peter. **Inteligência artificial**. Rio de Janeiro: Elsevier, c2013. xxi, 988 p. ISBN 9788535237016._



# APÊNDICES

**Colocar link:**

Do código (armazenado no repositório);

Dos artefatos (armazenado do repositório);

Da apresentação final (armazenado no repositório);

Do vídeo de apresentação (armazenado no repositório).




