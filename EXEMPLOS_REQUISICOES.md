# EXEMPLOS DE REQUISIÇÕES - HOTEL RESERVATION API

## 1. CUSTOMERS (Clientes)

### 1.1 Criar Cliente (POST)
**Endpoint:** POST http://localhost:8080/api/customers
**Headers:** Content-Type: application/json
**Body:**
```json
{
  "name": "João Silva",
  "email": "joao.silva@email.com",
  "phone": "11999999999",
  "address": {
    "zipCode": "01310-100",
    "street": "Avenida Paulista",
    "addressDetails": "Apto 101",
    "neighborhood": "Bela Vista",
    "state": "SP"
  }
}
```

### 1.2 Listar Todos os Clientes (GET)
**Endpoint:** GET http://localhost:8080/api/customers
**Headers:** Content-Type: application/json

### 1.3 Buscar Cliente por ID (GET)
**Endpoint:** GET http://localhost:8080/api/customers/1
**Headers:** Content-Type: application/json

### 1.4 Atualizar Cliente (PUT)
**Endpoint:** PUT http://localhost:8080/api/customers/1
**Headers:** Content-Type: application/json
**Body:**
```json
{
  "name": "João Silva Santos",
  "email": "joao.silva@email.com",
  "phone": "11988888888",
  "address": {
    "zipCode": "01310-100",
    "street": "Avenida Paulista",
    "addressDetails": "Apto 102",
    "neighborhood": "Bela Vista",
    "state": "SP"
  }
}
```

### 1.5 Deletar Cliente (DELETE)
**Endpoint:** DELETE http://localhost:8080/api/customers/1
**Headers:** Content-Type: application/json

---

## 2. ROOMS (Quartos)

### 2.1 Criar Quarto (POST)
**Endpoint:** POST http://localhost:8080/api/rooms
**Headers:** Content-Type: application/json
**Body:**
```json
{
  "number": "101",
  "type": "Standard",
  "pricePerNight": 200.00,
  "capacity": 2,
  "available": true
}
```

### 2.2 Criar Quarto Luxo (POST)
**Endpoint:** POST http://localhost:8080/api/rooms
**Headers:** Content-Type: application/json
**Body:**
```json
{
  "number": "201",
  "type": "Deluxe",
  "pricePerNight": 450.00,
  "capacity": 4,
  "available": true
}
```

### 2.3 Listar Todos os Quartos (GET)
**Endpoint:** GET http://localhost:8080/api/rooms
**Headers:** Content-Type: application/json

### 2.4 Buscar Quarto por ID (GET)
**Endpoint:** GET http://localhost:8080/api/rooms/1
**Headers:** Content-Type: application/json

### 2.5 Listar Quartos Disponíveis (GET)
**Endpoint:** GET http://localhost:8080/api/rooms/available
**Headers:** Content-Type: application/json

### 2.6 Atualizar Quarto (PUT)
**Endpoint:** PUT http://localhost:8080/api/rooms/1
**Headers:** Content-Type: application/json
**Body:**
```json
{
  "number": "101",
  "type": "Standard Plus",
  "pricePerNight": 250.00,
  "capacity": 2,
  "available": true
}
```

### 2.7 Deletar Quarto (DELETE)
**Endpoint:** DELETE http://localhost:8080/api/rooms/1
**Headers:** Content-Type: application/json

---

## 3. RESERVATIONS (Reservas)

### 3.1 Criar Reserva (POST)
**Endpoint:** POST http://localhost:8080/api/reservations
**Headers:** Content-Type: application/json
**Body:**
```json
{
  "customerId": 1,
  "roomId": 1,
  "checkInDate": "2026-02-15",
  "checkOutDate": "2026-02-18"
}
```

### 3.2 Encerrar Reserva (PATCH)
**Endpoint:** PATCH http://localhost:8080/api/reservations/1/close
**Headers:** Content-Type: application/json

### 3.3 Buscar Reservas por Período (GET)
**Endpoint:** GET http://localhost:8080/api/reservations/by-date-range?startDate=2026-02-01&endDate=2026-02-28
**Headers:** Content-Type: application/json
**Query Params:**
- startDate: 2026-02-01
- endDate: 2026-02-28

### 3.4 Listar Quartos Ocupados no Momento (GET)
**Endpoint:** GET http://localhost:8080/api/reservations/occupied-rooms
**Headers:** Content-Type: application/json

---

## FLUXO COMPLETO DE TESTE

### Passo 1: Criar um cliente
POST http://localhost:8080/api/customers
```json
{
  "name": "Maria Oliveira",
  "email": "maria.oliveira@email.com",
  "phone": "21987654321",
  "address": {
    "zipCode": "20040-020",
    "street": "Avenida Rio Branco",
    "addressDetails": "Sala 501",
    "neighborhood": "Centro",
    "state": "RJ"
  }
}
```

### Passo 2: Criar um quarto
POST http://localhost:8080/api/rooms
```json
{
  "number": "305",
  "type": "Suite",
  "pricePerNight": 350.00,
  "capacity": 3,
  "available": true
}
```

### Passo 3: Criar uma reserva
POST http://localhost:8080/api/reservations
```json
{
  "customerId": 1,
  "roomId": 1,
  "checkInDate": "2026-03-10",
  "checkOutDate": "2026-03-15"
}
```

### Passo 4: Verificar quartos ocupados
GET http://localhost:8080/api/reservations/occupied-rooms

### Passo 5: Encerrar a reserva
PATCH http://localhost:8080/api/reservations/1/close

---

## ACESSO AO SWAGGER
**URL:** http://localhost:8080/swagger-ui.html

## ACESSO AO H2 CONSOLE
**URL:** http://localhost:8080/h2-console
**JDBC URL:** jdbc:h2:mem:hoteldb
**Username:** sa
**Password:** (deixar em branco)

---

## OBSERVAÇÕES

1. Todas as requisições devem ter o header: Content-Type: application/json
2. As datas devem estar no formato ISO: YYYY-MM-DD
3. O cache tem TTL de 30 segundos nas operações de leitura
4. Ao criar uma reserva, o quarto fica automaticamente indisponível
5. Ao encerrar uma reserva, o quarto volta a ficar disponível
6. Não é possível criar duas reservas para o mesmo quarto em períodos conflitantes
