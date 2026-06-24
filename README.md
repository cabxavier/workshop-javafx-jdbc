# 🖥️ Workshop JavaFX JDBC

![status](https://img.shields.io/badge/status-conclu%C3%ADdo-brightgreen?style=flat-square)
![Java](https://img.shields.io/badge/Java-11-007396?style=flat-square&logo=openjdk&logoColor=white)
![JavaFX](https://img.shields.io/badge/JavaFX-FXML-1283C3?style=flat-square&logo=openjdk&logoColor=white)
![JDBC](https://img.shields.io/badge/JDBC-API-4DB33D?style=flat-square)
![MySQL](https://img.shields.io/badge/MySQL-8-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Eclipse](https://img.shields.io/badge/Eclipse-IDE-2C2255?style=flat-square&logo=eclipseide&logoColor=white)

Aplicação **desktop** em **JavaFX** para gerenciar **vendedores** e **departamentos**, com persistência em **MySQL** via **JDBC** e padrão **DAO**. CRUD completo, telas em **FXML**, validação de formulários com mensagens por campo e notificação de mudanças entre telas via *listeners*.

---

## 📑 Sumário

- [Funcionalidades](#-funcionalidades)
- [Conceitos aplicados](#-conceitos-aplicados)
- [Tecnologias](#-tecnologias)
- [Estrutura do projeto](#-estrutura-do-projeto)
- [Configuração](#-configuração)
- [Como executar](#-como-executar)
- [Crédito](#-crédito)

---

## ✨ Funcionalidades

- **CRUD de Departamentos** e **CRUD de Vendedores** (criar, listar, editar e remover).
- **Validação de formulários** com mensagens de erro por campo (nome, e-mail, data de nascimento, salário).
- **ComboBox** de departamentos no cadastro de vendedor.
- **Alertas** de confirmação e de erro, incluindo tratamento amigável de **violação de integridade referencial** ao remover.
- Atualização automática das tabelas após cada operação (padrão *Observer* com `DataChangeListener`).

---

## 📚 Conceitos aplicados

- **JavaFX + FXML**: separação entre layout (`.fxml`) e lógica (controllers).
- **MVC em camadas**: `gui` (apresentação), `model.services` (negócio), `model.dao` (acesso a dados), `model.entities` (domínio).
- **Padrão DAO + Factory**: interfaces (`SellerDao`, `DepartmentDao`), implementações JDBC e `DaoFactory`.
- **Padrão Observer**: `DataChangeListener` notifica as listas quando um formulário salva dados.
- **Tratamento de exceções**: `DbException`, `DbIntegrityException` (violação de FK) e `ValidationException` (erros de formulário por campo).
- **Injeção de dependência manual** dos *services* nos controllers.

---

## 🛠 Tecnologias

| Tecnologia | Descrição |
|------------|-----------|
| **Java 11** | Linguagem principal |
| **JavaFX** | Framework de interface gráfica (FXML) |
| **JDBC** | API de acesso a banco de dados |
| **MySQL** | Banco de dados relacional |
| **MySQL Connector/J** | Driver JDBC do MySQL |
| **Eclipse IDE / Scene Builder** | Desenvolvimento e edição dos FXML |

---

## 📂 Estrutura do projeto

```
src/
├── application/
│   ├── Main.java              # Ponto de entrada JavaFX (carrega MainView)
│   └── application.css        # Estilos
├── db/
│   ├── DB.java                # Conexão, leitura do db.properties, fechamento de recursos
│   ├── DbException.java       # Exceção genérica de banco
│   └── DbIntegrityException.java  # Violação de integridade referencial
├── gui/                       # Camada de apresentação (controllers + FXML)
│   ├── MainViewController + MainView.fxml
│   ├── SellerList/SellerForm (+ controllers e FXML)
│   ├── DepartmentList/DepartmentForm (+ controllers e FXML)
│   ├── About.fxml
│   ├── listeners/DataChangeListener.java   # Observer
│   └── util/                  # Alerts, Constraints, Utils
└── model/
    ├── entities/              # Seller, Department
    ├── dao/                   # SellerDao, DepartmentDao, DaoFactory, impl/ (JDBC)
    ├── services/              # SellerService, DepartmentService
    └── exceptions/            # ValidationException
```

---

## ⚙️ Configuração

As credenciais ficam em `db.properties` na raiz do projeto, **que não é versionado** (está no `.gitignore`). Use o template:

```bash
cp db.properties.example db.properties
```

E edite com seus dados reais:

```properties
user=SEU_USUARIO
password=SUA_SENHA
dburl=jdbc:mysql://localhost:3306/coursejdbc
useSSL=false
```

> 🔒 Nunca comite o `db.properties` com credenciais reais — apenas o `db.properties.example`.

---

## ▶️ Como executar

**Pré-requisitos:** JDK 11+, **JavaFX SDK**, **MySQL Connector/J** e MySQL em execução.

1. Crie o banco `coursejdbc` com as tabelas `department` e `seller`.
2. Copie e configure o `db.properties` (ver acima).
3. Adicione o **JavaFX SDK** e o **MySQL Connector/J** ao classpath/módulos do projeto.
4. Execute `application.Main`.

No Eclipse, configure as VM args do JavaFX, por exemplo:

```
--module-path "CAMINHO_DO_JAVAFX/lib" --add-modules javafx.controls,javafx.fxml
```

---

## 👤 Crédito

Projeto desenvolvido por **César Augusto Barbosa Xavier** como exercício do curso de Java (seção de JavaFX / JDBC) de **Nélio Alves**.
