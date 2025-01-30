SET timezone TO 'UTC';
CREATE DATABASE db_autoescola;


CREATE TABLE aula (
  Id_Aula SERIAL PRIMARY KEY,
  data_Aula VARCHAR(20) NOT NULL,
  hora_Inicio VARCHAR(20) NOT NULL,
  hora_Fim VARCHAR(20) NOT NULL,
  id_Veiculo INT REFERENCES automovel(Id_Veiculo) ON DELETE SET NULL,
  id_Instrutor INT REFERENCES funcionario(Id_Func) ON DELETE SET NULL
);


CREATE TABLE automovel (
  Id_Veiculo SERIAL PRIMARY KEY,
  placa VARCHAR(15) NOT NULL,
  ano VARCHAR(10) NOT NULL,
  modelo VARCHAR(25) NOT NULL,
  capacidade INT NOT NULL,
  status BOOLEAN NOT NULL
);

-- Inserindo dados na tabela `automovel`
INSERT INTO automovel (placa, ano, modelo, capacidade, status) VALUES
('111-1111', '1111', '1111', 1, TRUE),
('222-2222', '2222', '2', 1, TRUE),
('333-3333', '3333', '3333', 333331, TRUE);


CREATE TABLE cliente (
  Id_Cliente SERIAL PRIMARY KEY,
  Id_Endereco INT REFERENCES endereco(Id_Endereco),
  nome VARCHAR(50) NOT NULL,
  cel VARCHAR(50) NOT NULL,
  data_Nasc VARCHAR(40) NOT NULL,
  rg VARCHAR(50) NOT NULL,
  cpf VARCHAR(50) NOT NULL,
  status BOOLEAN NOT NULL,
  categoria VARCHAR(50) NOT NULL
);




CREATE TABLE endereco (
  Id_Endereco SERIAL PRIMARY KEY,
  num VARCHAR(10) NOT NULL,
  cidade VARCHAR(20) NOT NULL,
  estado VARCHAR(50) NOT NULL,
  logradouro VARCHAR(30) NOT NULL,
  bairro VARCHAR(20) NOT NULL,
  cep VARCHAR(20) NOT NULL,
  status BOOLEAN NOT NULL
  );



  CREATE TABLE funcionario (
  Id_Func SERIAL PRIMARY KEY,
  Id_Endereco INT REFERENCES endereco(Id_Endereco),
  rg VARCHAR(12) NOT NULL,
  nome VARCHAR(50) NOT NULL,
  cpf VARCHAR(14) NOT NULL,
  dataNasc VARCHAR(20) NOT NULL,
  cel VARCHAR(30) NOT NULL,
  status BOOLEAN NOT NULL,
  tipo VARCHAR(10) NOT NULL,
  carteira VARCHAR(20),
  categoria VARCHAR(10)
);

CREATE TABLE login (
  Id_Login SERIAL PRIMARY KEY,
  login VARCHAR(25) NOT NULL,
  senha VARCHAR(25) NOT NULL,
  status BOOLEAN NOT NULL,
  Id_Func INT REFERENCES funcionario(Id_Func)
);

CREATE TABLE clienteaula (
  Id_Aula INT REFERENCES aula(Id_Aula) ON DELETE CASCADE,
  Id_Cliente INT REFERENCES cliente(Id_Cliente) ON DELETE CASCADE,
  presenca BOOLEAN NOT NULL,
  PRIMARY KEY (Id_Aula, Id_Cliente)
);
