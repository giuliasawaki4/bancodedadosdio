-- Criação do banco de dados (opcional, dependendo do SGBD)
CREATE DATABASE ecommerce;
USE ecommerce;

-- Tabela Cliente
CREATE TABLE clients(
    idClient INT PRIMARY KEY AUTO_INCREMENT,
    -- ...
);

-- Tabela Cliente PF (Relacionamento 1 para 1 com a tabela cliente)
CREATE TABLE clients_pf(
    idClientPf INT PRIMARY KEY,
    cpf CHAR(11) NOT NULL,
    -- ...
    CONSTRAINT fk_client_pf FOREIGN KEY (idClientPf) REFERENCES clients(idClient)
);

-- Tabela Cliente PJ (Relacionamento 1 para 1 com a tabela cliente)
CREATE TABLE clients_pj(
    idClientPj INT PRIMARY KEY,
    cnpj CHAR(14) NOT NULL,
    -- ...
    CONSTRAINT fk_client_pj FOREIGN KEY (idClientPj) REFERENCES clients(idClient)
);

-- Tabela Pagamento (um cliente pode ter vários pagamentos)
CREATE TABLE payments(
    idPayment INT PRIMARY KEY AUTO_INCREMENT,
    idPaymentClient INT,
    type_of_payment ENUM('Crédito', 'Débito', 'Boleto', 'PIX'),
    card_number VARCHAR(16),
    -- ...
    CONSTRAINT fk_payments_client FOREIGN KEY (idPaymentClient) REFERENCES clients(idClient)
);

-- Tabela Entrega
CREATE TABLE deliveries(
    idDelivery INT PRIMARY KEY AUTO_INCREMENT,
    status ENUM('Processando', 'Enviado', 'Entregue', 'Cancelado') DEFAULT 'Processando',
    tracking_code VARCHAR(45) UNIQUE,
    -- ...
);
