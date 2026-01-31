# Hotel Reservation API

Sistema de gerenciamento de reservas de hotel desenvolvido com Spring Boot.

## 🚀 Tecnologias Utilizadas

- Java 17
- Spring Boot 3.1.5
- Spring Data JPA
- Hibernate
- H2 Database (em memória)
- Spring Cache (Caffeine)
- JUnit 5 e Mockito
- Swagger/OpenAPI
- Lombok
- Maven

## 📋 Requisitos

- Java 17 ou superior
- Maven 3.6+

## 🔧 Instalação e Execução

### 1. Clonar o repositório
```bash
git clone <url-do-repositorio>
cd hotel-reservation-api
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

## 📚 Documentação da API

Após iniciar a aplicação, acesse:

- **Swagger UI**: http://localhost:8080/swagger-ui.html
- **H2 Console**: http://localhost:8080/h2-console
  - JDBC URL: `jdbc:h2:mem:hoteldb`
  - Username: `sa`
  - Password: (deixar em branco)

## 🏗️ Estrutura do Projeto

```
src/
├── main/
│   ├── java/com/hotel/
│   │   ├── config/          # Configurações (Cache)
│   │   ├── controller/      # Controllers REST
│   │   ├── dto/             # Data Transfer Objects
│   │   ├── entity/          # Entidades JPA
│   │   ├── exception/       # Tratamento de exceções
│   │   ├── mapper/          # Conversão Entity <-> DTO
│   │   ├── repository/      # Repositórios JPA
│   │   └── service/         # Regras de negócio
│   └── resources/
│       └── application.properties
└── test/
    └── java/com/hotel/service/  # Testes unitários
```

## 🎯 Funcionalidades Implementadas

### Customers (Clientes)
- ✅ Criar cliente com endereço
- ✅ Listar todos os clientes
- ✅ Buscar cliente por ID
- ✅ Atualizar cliente
- ✅ Deletar cliente

### Rooms (Quartos)
- ✅ Criar quarto
- ✅ Listar todos os quartos
- ✅ Buscar quarto por ID
- ✅ Atualizar quarto
- ✅ Deletar quarto
- ✅ Listar quartos disponíveis

### Reservations (Reservas)
- ✅ Abrir nova reserva
- ✅ Encerrar reserva
- ✅ Buscar reservas por intervalo de datas
- ✅ Visualizar quartos ocupados no momento

## 🗄️ Modelo de Dados

### Tabelas
- **customers**: Dados dos clientes
- **address**: Endereços dos clientes (1:1 com customers)
- **rooms**: Quartos do hotel
- **reservations**: Reservas realizadas

### Relacionamentos
- Customer 1:1 Address
- Reservation N:1 Customer
- Reservation N:1 Room

## ⚡ Cache

Implementado com Caffeine:
- **TTL**: 30 segundos
- **Caches**: customers, rooms, reservations
- **Aplicado em**: Todas as operações de leitura (GET)

## 📝 Logs

Todos os endpoints possuem logs implementados para facilitar troubleshooting:
- INFO: Operações bem-sucedidas
- ERROR: Erros e exceções

## 🧪 Testes Unitários

Testes implementados para os serviços:
- CustomerServiceTest
- RoomServiceTest
- ReservationServiceTest

Cobertura de cenários:
- ✅ Criação de registros
- ✅ Listagem de registros
- ✅ Atualização de registros
- ✅ Deleção de registros
- ✅ Validações de regras de negócio
- ✅ Tratamento de exceções

## 🔀 GitFlow

O projeto segue o modelo GitFlow:
- **main**: Produção
- **develop**: Desenvolvimento
- **feature/**: Novas funcionalidades
- **hotfix/**: Correções urgentes

## 💡 Sugestão de Melhoria (Resposta ao Tech Lead)

Durante a cerimônia de refinamento, sugiro a seguinte melhoria para agregar mais valor ao cliente:

### Integração com API de CEP (ViaCEP)

**Problema identificado:**
Atualmente, o cliente precisa digitar manualmente todos os dados do endereço (rua, bairro, estado), o que pode gerar:
- Erros de digitação
- Inconsistência nos dados
- Experiência ruim para o usuário

**Solução proposta:**
Integrar com a API pública do ViaCEP (https://viacep.com.br/):

1. Cliente informa apenas o CEP
2. Sistema busca automaticamente:
   - Logradouro (rua)
   - Bairro
   - Cidade
   - Estado
3. Cliente confirma ou ajusta apenas o complemento (número, apto)

**Benefícios:**
- ✅ **Redução de erros**: Dados padronizados e validados
- ✅ **Melhor UX**: Menos campos para preencher
- ✅ **Dados confiáveis**: Endereços corretos para correspondência
- ✅ **Agilidade**: Cadastro mais rápido

**Implementação:**
- Endpoint adicional: `GET /api/addresses/cep/{cep}`
- Retorna dados preenchidos do endereço
- Frontend preenche automaticamente os campos
- Baixo custo e fácil manutenção (API gratuita)

**Exemplo de uso:**
```
GET /api/addresses/cep/01310-100

Retorna:
{
  "zipCode": "01310-100",
  "street": "Avenida Paulista",
  "neighborhood": "Bela Vista",
  "city": "São Paulo",
  "state": "SP"
}
```

Essa melhoria agregaria muito valor com pouco esforço de desenvolvimento!

## 📧 Contato

Para dúvidas ou sugestões sobre o projeto, entre em contato.

---

**Desenvolvido como parte do desafio técnico para vaga de estágio em Back-End**
