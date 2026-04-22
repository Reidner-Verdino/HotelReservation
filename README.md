# 🏨 Hotel Reservation API

Sistema de gerenciamento de reservas de hotel desenvolvido com **Spring Boot**, seguindo boas práticas de arquitetura REST, cache, testes unitários e documentação automática via Swagger.

> Desenvolvido como parte do desafio técnico para vaga de estágio em Back-End.

---

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Versão | Uso |
|---|---|---|
| Java | 17 | Linguagem principal |
| Spring Boot | 3.1.5 | Framework principal |
| Spring Data JPA | — | Persistência de dados |
| Hibernate | — | ORM |
| H2 Database | — | Banco de dados em memória |
| Spring Cache (Caffeine) | — | Cache de leitura (TTL 30s) |
| JUnit 5 + Mockito | — | Testes unitários |
| Swagger / OpenAPI | 2.2.0 | Documentação da API |
| Lombok | — | Redução de boilerplate |
| Maven | 3.6+ | Gerenciador de dependências |

---

## 📋 Pré-requisitos

- Java 17 ou superior
- Maven 3.6+

---

## 🚀 Como Executar

### 1. Clonar o repositório
```bash
git clone https://github.com/Reidner-Verdino/HotelReservation.git
cd HotelReservation
```

### 2. Compilar o projeto
```bash
mvn clean install
```

### 3. Executar a aplicação
```bash
mvn spring-boot:run
```

A aplicação estará disponível em: `http://localhost:8080`

### 4. Executar os testes
```bash
mvn test
```

---

## 📚 Documentação e Ferramentas

Após iniciar a aplicação, acesse:

| Ferramenta | URL |
|---|---|
| **Swagger UI** | http://localhost:8080/swagger-ui.html |
| **H2 Console** | http://localhost:8080/h2-console |

**Configurações do H2 Console:**
- JDBC URL: `jdbc:h2:mem:hoteldb`
- Username: `sa`
- Password: *(deixar em branco)*

---

## 🏗️ Estrutura do Projeto

```
HotelReservation/
├── src/
│   ├── main/
│   │   ├── java/com/hotel/
│   │   │   ├── config/        # Configurações (Cache)
│   │   │   ├── controller/    # Controllers REST
│   │   │   ├── dto/           # Data Transfer Objects
│   │   │   ├── entity/        # Entidades JPA
│   │   │   ├── exception/     # Tratamento de exceções
│   │   │   ├── mapper/        # Conversão Entity <-> DTO
│   │   │   ├── repository/    # Repositórios JPA
│   │   │   └── service/       # Regras de negócio
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       └── java/com/hotel/service/  # Testes unitários
├── EXEMPLOS_REQUISICOES.md    # Exemplos de chamadas à API
├── POSTMAN_COLLECTION.json    # Coleção pronta para importar no Postman
├── pom.xml                    # Dependências Maven
└── README.md                  # Este arquivo
```

---

## 🎯 Endpoints Disponíveis

### 👤 Customers (Clientes)
| Método | Endpoint | Descrição |
|---|---|---|
| POST | `/api/customers` | Criar cliente |
| GET | `/api/customers` | Listar todos |
| GET | `/api/customers/{id}` | Buscar por ID |
| PUT | `/api/customers/{id}` | Atualizar cliente |
| DELETE | `/api/customers/{id}` | Deletar cliente |

### 🛏️ Rooms (Quartos)
| Método | Endpoint | Descrição |
|---|---|---|
| POST | `/api/rooms` | Criar quarto |
| GET | `/api/rooms` | Listar todos |
| GET | `/api/rooms/{id}` | Buscar por ID |
| GET | `/api/rooms/available` | Listar disponíveis |
| PUT | `/api/rooms/{id}` | Atualizar quarto |
| DELETE | `/api/rooms/{id}` | Deletar quarto |

### 📅 Reservations (Reservas)
| Método | Endpoint | Descrição |
|---|---|---|
| POST | `/api/reservations` | Abrir nova reserva |
| PATCH | `/api/reservations/{id}/close` | Encerrar reserva |
| GET | `/api/reservations/by-date-range` | Buscar por período |
| GET | `/api/reservations/occupied-rooms` | Quartos ocupados agora |

---

## 🗄️ Modelo de Dados

### Entidades
- **customers** — Dados dos clientes
- **address** — Endereços (1:1 com customers)
- **rooms** — Quartos do hotel
- **reservations** — Reservas realizadas

### Relacionamentos
```
Customer ──1:1── Address
Reservation ──N:1── Customer
Reservation ──N:1── Room
```

---

## ⚡ Cache

Implementado com **Caffeine**:
- **TTL**: 30 segundos
- **Caches**: `customers`, `rooms`, `reservations`
- **Aplicado em**: Todas as operações de leitura (GET)

---

## 🧪 Testes Unitários

Cobertura implementada para os serviços:

| Serviço | Cenários testados |
|---|---|
| `CustomerServiceTest` | CRUD + validações + exceções |
| `RoomServiceTest` | CRUD + disponibilidade + exceções |
| `ReservationServiceTest` | Abertura/encerramento + conflitos de datas |

---

## 🔀 GitFlow

O projeto segue o modelo GitFlow:

| Branch | Finalidade |
|---|---|
| `main` | Código de produção estável |
| `develop` | Integração de novas funcionalidades |
| `feature/*` | Desenvolvimento de novas features |
| `hotfix/*` | Correções urgentes em produção |

---

## 💡 Sugestão de Melhoria — Integração com ViaCEP

### Problema identificado
Atualmente o cliente precisa digitar manualmente todos os dados do endereço, o que pode gerar erros de digitação, inconsistência nos dados e experiência ruim.

### Solução proposta
Integrar com a API pública do [ViaCEP](https://viacep.com.br/):

1. Cliente informa apenas o **CEP**
2. Sistema busca automaticamente: logradouro, bairro, cidade e estado
3. Cliente preenche apenas o complemento (número, apto)

### Novo endpoint sugerido

```
GET /api/addresses/cep/{cep}
```

**Resposta:**
```json
{
  "zipCode": "01310-100",
  "street": "Avenida Paulista",
  "neighborhood": "Bela Vista",
  "city": "São Paulo",
  "state": "SP"
}
```

### Benefícios
- ✅ Redução de erros de digitação
- ✅ Dados padronizados e validados
- ✅ Cadastro mais rápido (menos campos)
- ✅ API gratuita, sem custo adicional

---

## 📧 Contato

Para dúvidas ou sugestões, entre em contato com **Reidner Verdino**.
