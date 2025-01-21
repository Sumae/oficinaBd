# oficinaBd
-- Tabela de Clientes
CREATE TABLE Cliente (
    idCliente INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100),
    cpf_cnpj VARCHAR(20) UNIQUE,
    telefone VARCHAR(15),
    endereco VARCHAR(255)
);

-- Tabela de Veículos
CREATE TABLE Veiculo (
    idVeiculo INT AUTO_INCREMENT PRIMARY KEY,
    placa VARCHAR(10) UNIQUE,
    modelo VARCHAR(50),
    ano INT,
    cor VARCHAR(20),
    idCliente INT,
    FOREIGN KEY (idCliente) REFERENCES Cliente(idCliente)
);

-- Tabela de Serviços
CREATE TABLE Servico (
    idServico INT AUTO_INCREMENT PRIMARY KEY,
    tipo VARCHAR(50),
    descricao TEXT,
    preco DECIMAL(10, 2)
);

-- Tabela de Funcionários
CREATE TABLE Funcionario (
    idFuncionario INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100),
    cpf VARCHAR(20) UNIQUE,
    cargo VARCHAR(50),
    salario DECIMAL(10, 2)
);

-- Tabela de Ordens de Serviço (OS)
CREATE TABLE OrdemServico (
    idOrdemServico INT AUTO_INCREMENT PRIMARY KEY,
    data DATE,
    status VARCHAR(50),
    valor_total DECIMAL(10, 2),
    idVeiculo INT,
    FOREIGN KEY (idVeiculo) REFERENCES Veiculo(idVeiculo)
);

-- Tabela de Relação entre Ordem de Serviço e Serviços
CREATE TABLE OrdemServico_Servico (
    idOrdemServico INT,
    idServico INT,
    quantidade INT,
    PRIMARY KEY (idOrdemServico, idServico),
    FOREIGN KEY (idOrdemServico) REFERENCES OrdemServico(idOrdemServico),
    FOREIGN KEY (idServico) REFERENCES Servico(idServico)
);

-- Tabela de Relação entre Ordem de Serviço e Funcionários
CREATE TABLE OrdemServico_Funcionario (
    idOrdemServico INT,
    idFuncionario INT,
    PRIMARY KEY (idOrdemServico, idFuncionario),
    FOREIGN KEY (idOrdemServico) REFERENCES OrdemServico(idOrdemServico),
    FOREIGN KEY (idFuncionario) REFERENCES Funcionario(idFuncionario)
);



-- Inserindo clientes
INSERT INTO Cliente (nome, cpf_cnpj, telefone, endereco)
VALUES ('João Silva', '123.456.789-00', '11987654321', 'Rua A, 123');

-- Inserindo veículos
INSERT INTO Veiculo (placa, modelo, ano, cor, idCliente)
VALUES ('ABC-1234', 'Civic', 2020, 'Preto', 1);

-- Inserindo serviços
INSERT INTO Servico (tipo, descricao, preco)
VALUES ('Troca de óleo', 'Troca de óleo completa', 150.00),
       ('Alinhamento', 'Alinhamento e balanceamento', 100.00);

-- Inserindo funcionários
INSERT INTO Funcionario (nome, cpf, cargo, salario)
VALUES ('Carlos Mendes', '987.654.321-00', 'Mecânico', 3000.00);

-- Inserindo ordem de serviço
INSERT INTO OrdemServico (data, status, valor_total, idVeiculo)
VALUES ('2025-01-20', 'Concluída', 250.00, 1);

-- Relacionando ordem de serviço e serviços
INSERT INTO OrdemServico_Servico (idOrdemServico, idServico, quantidade)
VALUES (1, 1, 1), (1, 2, 1);

-- Relacionando ordem de serviço e funcionário
INSERT INTO OrdemServico_Funcionario (idOrdemServico, idFuncionario)
VALUES (1, 1);
