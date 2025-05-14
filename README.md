# SQL

Hoje, na aula de Banco de Dados com a professora Flávia Maria Alves Lopes, aprendemos: 
- CHECK, 
- CONSTRAINT, 
- NOT NULL, 
- UNIQUE, 
- PRIMARY KEY, 
- FOREIGN KEY.

--------------------------------------------------------------------------------------------------

CREATE TABLE produto
(
  produto_num INTEGER PRIMARY KEY,
  nome_produto VARCHAR(30) UNIQUE NOT NULL,
  preco_produto NUMERIC,
  preco_desconto NUMERIC,

  CONSTRAINT preco_positivo CHECK (preco_produto>0),
  CONSTRAINT preco_desconto_positivo CHECK (preco_desconto>0),
  CONSTRAINT desconto_valido CHECK (preco_produto > preco_desconto) 
);

INSERT INTO produto(produto_num,nome_produto, preco_produto, preco_desconto)
VALUES
(1, 'chocolate', 2 , 1 ),
(2, 'borracha', 2, 1);

--------------------------------------------------------------------------------------------------

CREATE TABLE pedidos
(
  id_pedido INTEGER PRIMARY KEY,
  data_pedido DATE,
  valor_total NUMERIC,
  valor_pago NUMERIC,
  produto_num INTEGER REFERENCES produto (produto_num),
  
  
  CONSTRAINT valor_pago_valido CHECK (valor_pago <= valor_total),
  CONSTRAINT valor_total_positivo CHECK (valor_total>=0),
  CONSTRAINT valor_pago_positivo CHECK (valor_pago >=0)
);

INSERT INTO pedidos (id_pedido, data_pedido, valor_total, valor_pago, produto_num)
VALUES
(10, '05/13/2025', 100, 100, 1);

--------------------------------------------------------------------------------------------------

CREATE TABLE funcionario
(
  id_funcionario INTEGER PRIMARY KEY,
  nome VARCHAR(50),
  salario NUMERIC CONSTRAINT salario_nao_negativo CHECK (salario>=0)
);

INSERT INTO funcionario (id_funcionario,nome, salario)
VALUES
(1, 'Pedro', 100);

--------------------------------------------------------------------------------------------------

CREATE TABLE clientes
(
  id_cliente INTEGER PRIMARY KEY,
  nome_cliente VARCHAR(50) NOT NULL,
  email VARCHAR(100)
);

INSERT INTO clientes (id_cliente, nome_cliente, email)
VALUES
(1, 'maria', 'maria@gmail.com');

--------------------------------------------------------------------------------------------------

CREATE TABLE emails
(
  id_email INTEGER PRIMARY KEY,
  endereco_email VARCHAR(100) UNIQUE NOT NULL
);

INSERT INTO emails /*(id_email, endereco_email)*/
VALUES
(1, 'm@m'),
(2, 'm@l');

--------------------------------------------------------------------------------------------------

CREATE TABLE cursos
(
  id_curso INTEGER PRIMARY KEY,
  nome_curso VARCHAR(100) UNIQUE NOT NULL,
  descricao TEXT 
);

INSERT INTO cursos (id_curso,nome_curso,descricao)
VALUES
(1, 'Direito', 'Leis'),
(2, 'Medicina', 'Medicos'),
(3, 'ADS', 'TI');

--------------------------------------------------------------------------------------------------

CREATE TABLE notas
(
  id_aluno INTEGER UNIQUE NOT NULL,
  id_disciplina VARCHAR(100) UNIQUE NOT NULL,
  nota NUMERIC ,
  frequencia INTEGER,
  PRIMARY KEY (id_aluno,id_disciplina)
);

INSERT INTO notas (id_aluno,id_disciplina,nota, frequencia)
VALUES
(1, 'Matematica', 5, 2);


