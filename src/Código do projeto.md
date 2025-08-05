# Código do projeto

Create database Novemp;
Use Novemp;

Create table Clientes (
ID_Cliente char(10) NOT NULL,
Nome char(40) NOT NULL,
CNPJ char(14),
InscriçãoEstadual char(15),
RazãoSocial char(40),
Email char(40),
CONSTRAINT CP_Clientes PRIMARY KEY (ID_Cliente),
CONSTRAINT UN_ClientesCNPJ UNIQUE (CNPJ),
CONSTRAINT UN_ClientesIE UNIQUE (InscriçãoEstadual),
CONSTRAINT UN_ClientesRS UNIQUE (RazãoSocial)
);

Create table EndereçoPagamento(
ID_EndereçoPag char(10) NOT NULL,
ID_Cliente char(10) NOT NULL,
Numero decimal(4),
Logradouro char(40),
Complemento char(20),
Estado char(40),
Cidade char(40),
Bairro char(40),
CONSTRAINT CP_EndPag PRIMARY KEY (ID_EndereçoPag),
CONSTRAINT CE_EndPag FOREIGN KEY (ID_Cliente) REFERENCES Clientes(ID_Cliente)
);

Create table EndereçoEntrega(
ID_EndereçoEnt char(10) NOT NULL,
ID_Cliente char(10) NOT NULL,
Numero decimal(4),
Logradouro char(40),
Complemento char(20),
Estado char(40),
Cidade char(40),
Bairro char(40),
CONSTRAINT CP_EndEnt PRIMARY KEY (ID_EndereçoEnt),
CONSTRAINT CE_EndEnt FOREIGN KEY (ID_Cliente) REFERENCES Clientes(ID_Cliente)
);

Create table Telefones(
ID_Telefone char(10) NOT NULL,
ID_Cliente char(10) NOT NULL,
DDD decimal(2),
Numero decimal(9),
Tipo char(20),
CONSTRAINT CP_Telefones PRIMARY KEY (ID_Telefone),
CONSTRAINT CE_Telefones FOREIGN KEY (ID_Cliente) REFERENCES Clientes(ID_Cliente)
);

Create table Representantes(
ID_Representantes char(10) NOT NULL,
Nome char(30),
CONSTRAINT CP_Representantes PRIMARY KEY (ID_Representantes)
);

Create table Contatos(
ID_Contatos char(10) NOT NULL,
Data date,
ID_Cliente char(10) NOT NULL,
ID_Representante char(10) NOT NULL,
CONSTRAINT CP_Contatos PRIMARY KEY (ID_Contatos),
CONSTRAINT CE_ContatosCliente FOREIGN KEY (ID_Cliente) REFERENCES Clientes(ID_Cliente),
CONSTRAINT CE_ContatosRepresentantes FOREIGN KEY (ID_Representante) REFERENCES Representantes(ID_Representantes)
);

Create table Pedidos(
ID_Pedidos char(10) NOT NULL,
ID_Cliente char(10) NOT NULL,
ID_Representante char(10) NOT NULL,
Comissão decimal(5,2),
PrazoEntrega decimal(3),
Frete decimal(10,2),
Data date,
Valor decimal(50,2),
QuantidadeParcelas decimal(2),
CONSTRAINT CP_Pedidos PRIMARY KEY (ID_Pedidos),
CONSTRAINT CE_PedidosCliente FOREIGN KEY (ID_Cliente) REFERENCES Clientes(ID_Cliente),
CONSTRAINT CE_PedidosRepresentantes FOREIGN KEY (ID_Representante) REFERENCES Representantes(ID_Representantes)
);

Create table Parcelas(
ID_Parcelas char(10) NOT NULL,
ID_Pedido char(10) NOT NULL,
FormaPagamento char(40),
Valor decimal(50,2),
DataPagamento date,
DataVencimento date,
CONSTRAINT CP_Parcelas PRIMARY KEY (ID_Parcelas),
CONSTRAINT CE_Parcelas FOREIGN KEY (ID_Pedido) REFERENCES Pedidos(ID_Pedidos)
);

Create table TiposProdutos(
ID_TiposProdutos char(10) NOT NULL,
Descrição char(100),
Categoria char(15),
CONSTRAINT CP_TiposProdutos PRIMARY KEY (ID_TiposProdutos)
);

Create table Produtos(
ID_Produtos char(10) NOT NULL,
ID_Tipo char(10) NOT NULL,
Nome char(50),
Valor decimal(50,2),
CONSTRAINT CP_Produtos PRIMARY KEY (ID_Produtos),
CONSTRAINT CE_Produtos FOREIGN KEY (ID_Tipo) REFERENCES TiposProdutos(ID_TiposProdutos)
);

Create table Itens(
ID_Itens char(10) NOT NULL,
ID_Pedido char(10) NOT NULL,
ID_Produto char(10) NOT NULL,
Nome char(50),
Quantidade decimal(5),
CONSTRAINT CP_Itens PRIMARY KEY (ID_Itens),
CONSTRAINT CE_ItensPedido FOREIGN KEY (ID_Pedido) REFERENCES Pedidos(ID_Pedidos),
CONSTRAINT CE_ItensProduto FOREIGN KEY (ID_Produto) REFERENCES Produtos(ID_Produtos)
);

ALTER TABLE itens CHANGE nome Nome char(50);
ALTER TABLE itens CHANGE quantidade Quantidade decimal(5);
ALTER TABLE parcelas CHANGE formapagamento FormaPagamento char(40);
ALTER TABLE parcelas CHANGE valor Valor decimal(12,2);
ALTER TABLE pedidos CHANGE comissao Comissao decimal(5,3);
ALTER TABLE pedidos CHANGE prazoentrega PrazoEntrega decimal(3);
ALTER TABLE pedidos CHANGE frete Frete decimal(12,2);
ALTER TABLE pedidos CHANGE valor Valor decimal(12,2);
ALTER TABLE pedidos CHANGE quantidadeparcelas QuantidadeParcelas decimal(2);
ALTER TABLE produtos CHANGE nome Nome char(50);
ALTER TABLE produtos CHANGE valor Valor decimal(12,2);
ALTER TABLE telefones CHANGE tipo Tipo char(50);
ALTER TABLE clientes CHANGE email Email char(40);
ALTER TABLE EndereçoEntrega CHANGE ID_EndereçoEnt ID_EnderecoEnt char(10) NOT NULL;
ALTER TABLE EndereçoPagamento CHANGE ID_EndereçoPag ID_EnderecoPag char(10) NOT NULL;
ALTER TABLE EndereçoPagamento CHANGE logradouro Logradouro char(50);
ALTER TABLE EndereçoPagamento CHANGE numero Numero decimal(4);
ALTER TABLE EndereçoPagamento CHANGE complemento Complemento char(30);
ALTER TABLE EndereçoPagamento CHANGE bairro Bairro char(40);
ALTER TABLE EndereçoPagamento CHANGE estado Estado char(30);
RENAME TABLE endereçoentrega TO enderecoentrega;
RENAME TABLE endereçopagamento TO enderecopagamento;

ALTER TABLE EndereçoPagamento MODIFY numero decimal(4) AFTER logradouro;
ALTER TABLE EndereçoPagamento MODIFY bairro char(40) AFTER numero;
ALTER TABLE EndereçoPagamento MODIFY estado char(30) AFTER cidade;
ALTER TABLE EndereçoPagamento MODIFY complemento char(30) AFTER numero;

ALTER TABLE EndereçoEntrega MODIFY numero decimal(4) AFTER logradouro;
ALTER TABLE EndereçoEntrega MODIFY bairro char(40) AFTER numero;
ALTER TABLE EndereçoEntrega MODIFY estado char(30) AFTER cidade;
ALTER TABLE EndereçoEntrega MODIFY complemento char(30) AFTER numero;

Script das instâncias do banco: 

insert into representantes values ('ttt1234567','Marco Paulo');
insert into representantes values ('ttu2400812','Lucas Rafael');
insert into representantes values ('tut0075678','Rafael Altaf');
insert into representantes values ('utt0000001','Hugo de Paula');
insert into representantes values ('ttu00113045','Felipe Lara');
insert into representantes values ('ttt8534671','Cristiano Araujo');

insert into clientes values ('aaa1511648', 'Anderson Babetto', '80737068000197', '5349340972911', 'Babetto LTDA','andersonbabetto13@outlook.com');
insert into clientes values ('aab6202345', 'Guilherme Briggs', '20793155000130', '0108148807025', 'Briggs House LTDA', 'guibriggs92@gmail.com');
insert into clientes values ('aaa1220006', 'Kauan H Guimaraes', '88638078000187', '3333582929678', 'Malhação Monstra ME', 'kauancanada@gmail.com');
insert into clientes values ('baa0072424', 'Filipe Simtob', '75923974000146', '6412013168043', 'RPG Pneus EPP', 'filipesimtob@yahoo.com');
insert into clientes values ('aaa5544613', 'Laura Neves', '18913732000138', '1742571458471', 'Viking Engenharia ME', 'lauraneves04@gmail.com');
insert into clientes values ('aaa2424221', 'Rafael Cabral', '90953460000127', '8606889888305', 'Cruzeiros do Sul Softwares ME', 'rafaelcabral00@outlook.com');
insert into clientes values ('aaa9863007', 'Vitor Fialho', '41854346000134', '8802016216330', 'Center Atlestismo LTDA', 'fialhocenter@gmail.com');
insert into clientes values ('aab0234581', 'Ettore Motta', '70501897000112', '5204336576907', 'Italia Moveis ME', 'ettoremottait@outlook.com');
insert into clientes values ('aba7641098', 'João Escochi', '67829690000167', '5515879724830', 'Penguin Poker SA', 'joaopedropoker@yahoo.com');
insert into clientes values ('baa8887663', 'Isaque Gomes' , '77784584000168', '3672551055688', 'Reverse Imoveis ME', 'isaqueimoveis@gmail.com');

insert into contatos values ('ccc1234567','2020-01-12','aaa1511648','ttt1234567');
insert into contatos values ('ccc1234568','2025-05-16','aaa1511648','ttu00113045');
insert into contatos values ('cdc0086754','2025-05-16','aab6202345','utt0000001');
insert into contatos values ('cdc0086755','2021-11-30','aaa1220006','ttu00113045');
insert into contatos values ('ccc4326901','2019-08-12','baa0072424','tut0075678');
insert into contatos values ('ddd9239401','2024-01-01','aaa5544613','ttt8534671');
insert into contatos values ('dcc6729101','2023-04-04','aaa2424221','ttt8534671');
insert into contatos values ('ccd0023421','2025-05-07','aaa2424221','ttu2400812');
insert into contatos values ('cdd0000001','2024-11-15','aaa9863007','ttt1234567');
insert into contatos values ('cdd2424242','2024-12-12','aba7641098','tut0075678');
insert into contatos values ('ccc3199700','2022-07-17','baa8887663','ttt1234567');
insert into contatos values ('ddd4002892','2023-07-19','aab0234581','utt0000001');

insert into TiposProdutos values ('xxy8463278', 'Gerenciamento de circuitos, proteção e medição de energia elétrica', 'quadro');
insert into TiposProdutos values ('yxx3696368', 'Alimentação elétrica para edifícios até 2600 A via rede aérea ou subterrânea', 'quadro') ;
insert into TiposProdutos values ('xyx9825493', 'Barramentos blindados de 1000 a 5000 A com baixa impedância e proteção IP31-55','barramento');
insert into TiposProdutos values ('yxy8158265', 'Energia para edifícios com carga acima de 2850 A em sistema estrela neutro','cabine');
insert into TiposProdutos values ('xxx7771777','projetados para otimizar a integração entre inversores, transformadores e painéis elétricos', 'Skid');


insert into Produtos values ('rrs9437864', 'xxy8463278', 'Quadro de Distribuição de Baixa Tensão', '2250');
insert into Produtos values ('srr5283749', 'yxx3696368', 'Quadro de Distribuição Compacto', '1380');
insert into Produtos values ('rsr9265409', 'xyx9825493', 'Barramento Blindado', '3250');
insert into Produtos values ('srs4833675', 'yxy8158265', 'Cabine de barramento', '820');
insert into Produtos values ('sss7878788', 'xxx7771777', 'Skid para Usinas Fotovoltaicas', '777.77');

insert into Pedidos values ('pqq5496325', 'aaa1511648', 'ttt1234567', '5.5', '15', '80.79', '2024-02-01','3150.49' , '1') ;
insert into Pedidos values ('qpp5698445', 'aaa2424221', 'ttu2400812', '6.3', '15', '85.87', '2025-05-18', '2285.97', '1') ;
insert into Pedidos values ('qpq8462597', 'aaa2424221', 'ttt8534671', '7.2', '17', '55.45', '2024-12-26', '3305.45', '2') ;
insert into Pedidos values ('pqp7346925', 'aab6202345', 'utt0000001', '5', '13', '46.36', '2025-01-30', '866.36', '1');
insert into Pedidos values ('ppq1795468', 'aaa1220006', 'ttu0011304', '6', '15', '35.57', '2024-04-09', '1415.57', '1');
insert into Pedidos values ('pqq4682599', 'baa0072424', 'tut0075678', '10',' 20', '85.96','2024-09-13', '4155.96', '1') ;
insert into Pedidos values ('qpp2546983', 'aba7641098', 'tut0075678', '5.25', '14', '55.68', '2024-07-01', '2255.68', '1');
insert into Pedidos values ('qpq5876329', 'aaa9863007', 'ttt1234567', '7', '15', '57.68', '2025-03-04', '1437.68', '1');
insert into Pedidos values ('qqp2658963', 'aaa5544613', 'ttt8534671', '7.8', '15', '39.65', '2025-04-01', '2289.65', '1');
insert into Pedidos values ('ppq6548932', 'aaa1511648', 'ttu0011304', '12', '19', '42.36', '2025-02-27', '5542.36', '1');
insert into Pedidos values ('pqq6854399', 'baa8887663', 'ttt1234567', '9', '14', '45.98', '2025-03-21', '865,98', '1');
insert into Pedidos values ('qqp1740877', 'aab0234581', 'utt0000001', '11', '21', '32,50', '2025-06-04', '1412,5', '1'); 

Insert into itens values ('lll0000001', 'pqq5496325', 'rrs9437864', 'Quadro de Distribuição de Baixa Tensão', '1');
Insert into itens values ('lll0000002', 'pqq5496325', 'srs4833675', 'Cabine de barramento', '1');
Insert into itens values ('lll0000003', 'qpp5698445', 'srs4833675', 'Cabine de barramento', '1');
Insert into itens values ('lll0000004', 'qpp5698445', 'srr5283749', 'Quadro de Distribuição Compacto', '1');
Insert into itens values ('lll0000005', 'qpq8462597', 'rsr9265409', 'Barramento Blindado', '1');
Insert into itens values ('lll0000006', 'pqp7346925', 'srs4833675', 'Cabine de barramento', '1');
Insert into itens values ('lll0000007', 'ppq1795468', 'srr5283749', 'Quadro de Distribuição Compacto', '1');
Insert into itens values ('mmm0000001', 'pqq4682599', 'rsr9265409', 'Barramento Blindado', '1');
Insert into itens values ('mmm0000002', 'pqq4682599', 'srs4833675', 'Cabine de barramento', '1');
Insert into itens values ('mmm0000003', 'qpp2546983', 'srr5283749', 'Cabine de barramento', '1');
Insert into itens values ('mmm0000004', 'qpp2546983', 'srs4833675', 'Cabine de barramento', '1');
Insert into itens values ('mmm0000005', 'qpq5876329', 'srr5283749', 'Quadro de Distribuição Compacto', '1');
Insert into itens values ('mmm0000006', 'qqp2658963', 'rrs9437864', 'Quadro de Distribuição de Baixa Tensão', '1');
Insert into itens values ('mmm0000007', 'ppq6548932', 'rrs9437864', 'Quadro de Distribuição de Baixa Tensão', '1');
Insert into itens values ('mmm0000008', 'ppq6548932', 'srr5283749', 'Quadro de Distribuição Compacto', '1');
Insert into itens values ('mmm0000009', 'pqq6854399', 'srs4833675', 'Cabine de barramento', '2');
Insert into itens values ('mmm0000010', 'qqp1740877', 'srr5283749', 'Quadro de Distribuição Compacto', '1');
   

INSERT INTO Parcelas VALUES ('nnn0000001', 'pqq5496325', 'Transferência', '3150.49', '2024-01-15', '2024-01-22');
INSERT INTO Parcelas VALUES ('nnn0000002', 'qpp5698445', 'Transferência', '2285.97', '2024-02-15', '2024-02-22');
INSERT INTO Parcelas VALUES ('nnn0000003', 'pqp7346925', 'Transferência', '866.36', '2024-03-15', '2024-03-22');
INSERT INTO Parcelas VALUES ('nnn0000004', 'ppq1795468', 'Transferência', '1415.57', '2024-06-11', '2024-06-18');
INSERT INTO Parcelas VALUES ('ooo0000001', 'pqq4682599', 'Transferência', '4155.96', '2024-07-08', '2024-07-10');
INSERT INTO Parcelas VALUES ('ooo0000002', 'qpp2546983', 'Transferência', '2255.68', '2024-07-01', '2024-07-02');
INSERT INTO Parcelas VALUES ('ooo0000003', 'qpq5876329', 'Transferência', '1437.68', '2025-03-05', '2025-03-04');
INSERT INTO Parcelas VALUES ('ooo0000004', 'qqp2658963', 'Pix', '2289.65', '2025-04-02', '2025-04-02');
INSERT INTO Parcelas VALUES ('ooo0000005', 'ppq6548932', 'Cartão', '5542.36', '2025-02-28', '2025-03-10');
INSERT INTO Parcelas VALUES ('ooo0000006', 'pqq6854399', 'Transferência', '1685.98', '2025-02-18', '2025-03-18');
INSERT INTO Parcelas VALUES ('ooo0000007', 'qpq8462597', 'Boleto', '1652.73', '2025-01-15', '2025-02-28');
INSERT INTO Parcelas VALUES ('ooo0000008', 'qpq8462597', 'Boleto', '1652.73', '2025-02-15', '2025-03-15');
INSERT INTO Parcelas VALUES ('ooo0000009', 'qqp1740877', 'Transferência', '1412.5', '2025-01-10', '2025-01-20');

Insert into EnderecoPagamento values ('eef2765489', 'aaa1511648', 'Rua Francisco Deslandes', '24', 'Casa', 'Anchieta', 'Belo horizonte', 'Minas Gerais');
Insert into EnderecoPagamento values ('eef2887901', 'aab6202345', 'Rua Augusta', '800', 'Apartamento 603', 'São Jose', 'Mauá', 'São Paulo');
Insert into EnderecoPagamento values ('eef2827002', 'aaa1220006', 'Av. Paulista', '70', 'Apartamento 101', 'Centro', 'Santo André', 'São Paulo');
Insert into EnderecoPagamento values ('eef2897962', 'baa0072424', 'Rua das Flores', '101', 'Casa', 'Santa Rosa', 'Niterói', 'Rio de Janeiro');
Insert into EnderecoPagamento values ('eef2087644', 'aaa5544613', 'Rua XV de Novembro', '503', 'Apartamento 405', 'Centro', 'São José dos Pinhais', 'Maranhão');
Insert into EnderecoPagamento values ('eef2183405', 'aaa2424221', 'Rua das Palmeiras', '1009', 'Casa', 'Itinga', 'Lauro de Freitas', 'Bahia');
Insert into EnderecoPagamento values ('eef2389876', 'aaa9863007', 'Av. Atlântica', '209', 'Cobertura 2', 'São José', 'Kobrasol', 'Paraná');
Insert into EnderecoPagamento values ('eef2987675', 'aab0234581', 'Rua Sete de Setembro', '5', 'Apartamento 302', 'Eldorado', 'Contagem', 'Minas Gerais');
Insert into EnderecoPagamento values ('eef2156308', 'aba7641098', 'Av. Brasil', '604', 'Casa', 'Centro', 'Canoas', 'Paraná');
Insert into EnderecoPagamento values ('eef2888684', 'baa8887663', 'Rua da Praia', '110','Apartamento 1501', 'Casa Caiada', 'Olinda', 'Bahia');

Insert into EnderecoEntrega values('jkj7897659', 'aaa1511648', 'Rua Francisco Deslandes', '24', 'Casa', 'Anchieta', 'Belo horizonte', 'Minas Gerais');
Insert into EnderecoEntrega values('jkj6758937', 'aab6202345', 'Rua Augusta', '800', 'Apartamento 603', 'São Jose', 'Mauá', 'São Paulo');
insert into EnderecoEntrega values('jkj7569453', 'baa0072424', 'Av. Paulista', '70', 'Apartamento 101', 'Centro',  'Santo André','São Paulo');
Insert into EnderecoEntrega values('jkj9076894', 'aaa1220006', 'Rua Augusta', '850', 'Apartamento 604', 'São Jose', 'Mauá', 'São Paulo');
Insert into EnderecoEntrega values('jkj8750941', 'aaa5544613', 'Av. Paulista', '70', 'Apartamento 102', 'Centro', 'Santo André', 'São Paulo');
Insert into EnderecoEntrega values('jkj1476587', 'aaa2424221', 'Rua XV de Novembro', '503', 'Apartamento 405', 'Centro', 'São José dos Pinhais', 'Maranhão');
Insert into EnderecoEntrega values('jkj6759341', 'aaa9863007', 'Rua XV de Novembro', '503', 'Apartamento 504', 'Centro', 'São José dos Pinhais', 'Maranhão');
Insert into EnderecoEntrega values('jkj9098065', 'aab0234581', 'Av. Atlântica', '209', 'Cobertura 2', 'Kobrasol', 'São José', 'Minas Gerais');
Insert into EnderecoEntrega values('jkj1686478', 'aba7641098', 'Av. Atlântica', '209', 'Cobertura 3', 'Kobrasol', 'São José', 'Minas Gerais');
Insert into EnderecoEntrega values('jkj5784113', 'baa8887663', 'Av. Brasil', '604', 'Casa', 'Centro', 'Canoas', 'Paraná');

Insert into Telefones values('vww8570943', 'aaa1511648', '031', '984178460', 'fixo');
insert into Telefones values('vww3849201', 'aab6202345', '011', '997462103', 'celular');
insert into Telefones values('vww4921867', 'aaa1220006', '071', '984736591', 'celular');
insert into Telefones values('vww7102389', 'baa0072424', '031', '996284037', 'celular');
insert into Telefones values('vww2387104', 'aaa5544613', '011', '991837402', 'celular');
insert into Telefones values('vww9871203', 'aaa2424221', '011', '998374625', 'celular');
insert into Telefones values('vww5601938', 'aaa9863007', '051', '985726193', 'celular');
insert into Telefones values('vww1049283', 'aab0234581', '062', '997382940', 'fixo');
insert into Telefones values('vww8392017', 'aba7641098', '031', '994820374', 'celular');
insert into Telefones values('vww2849301', 'baa8887663', '051', '999201837', 'celular');
