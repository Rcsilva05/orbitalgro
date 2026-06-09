# 🌱 OrbitAgro API

> Monitoramento Agrícola via Satélite e IoT — FIAP Global Solution 2026/1

OrbitAgro antecipa riscos agrícolas combinando imagens de satélite, índice NDVI e sensores IoT para que produtores rurais tomem decisões **antes** da perda da produção.

---

## 👥 Integrantes

| Nome | RM | Turma |
|------|----|-------|
| Seu Nome | RM00000 | 2TDS |

---

## 🔗 Links

| Item | Link |
|------|------|
| 🚀 Deploy | [em breve após deploy] |
| 📹 Vídeo de Apresentação | [em breve] |
| 🎯 Video Pitch | [em breve] |
| 📖 Swagger UI | `{url-deploy}/swagger-ui.html` |
| 📄 API Docs | `{url-deploy}/api-docs` |

---

## 🏗️ Arquitetura

```
orbitagro/
├── controller/     → Endpoints REST + HATEOAS
├── service/        → Regras de negócio
├── repository/     → JpaRepository
├── entity/         → Entidades JPA
├── dto/            → Java Records (Request/Response)
├── security/       → JWT + Spring Security
├── config/         → Swagger + CORS + Security
└── exception/      → GlobalExceptionHandler
```

---

## 🗄️ Modelo de Dados

```
TB_PRODUTOR
    ↓ 1:N
TB_AREA_CULTIVO
    ↓ 1:N          ↓ 1:N
TB_MONITORAMENTO  TB_ALERTA
```

---

## 🛠️ Tecnologias

- Java 17
- Spring Boot 3.2.5
- Spring Data JPA
- Spring Security + JWT
- Spring HATEOAS
- Spring Validation
- Lombok
- H2 Database
- Swagger / OpenAPI 3
- Maven

---

## ▶️ Como Executar

### Pré-requisitos
- Java 17+
- Maven 3.8+

### Passo a passo

```bash
# 1. Clonar o repositório
git clone https://github.com/seu-usuario/orbitagro.git

# 2. Entrar na pasta
cd orbitagro

# 3. Rodar o projeto
./mvnw spring-boot:run
```

A API estará disponível em: `http://localhost:8080`

---

## 🔐 Autenticação

### 1. Registrar usuário
```http
POST /auth/register
Content-Type: application/json

{
  "username": "admin",
  "password": "123456",
  "role": "ADMIN"
}
```

### 2. Fazer login
```http
POST /auth/login
Content-Type: application/json

{
  "username": "admin",
  "password": "123456"
}
```

Resposta:
```json
{
  "token": "eyJhbGciOiJIUzI1NiJ9...",
  "username": "admin",
  "role": "ADMIN"
}
```

### 3. Usar o token
Adicione no header de todas as requisições:
```
Authorization: Bearer {token}
```

---

## 📡 Endpoints

### Produtores
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/produtores` | Listar todos |
| GET | `/produtores/{id}` | Buscar por ID |
| POST | `/produtores` | Criar |
| PUT | `/produtores/{id}` | Atualizar |
| DELETE | `/produtores/{id}` | Deletar |

### Áreas de Cultivo
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/areas-cultivo` | Listar todas |
| GET | `/areas-cultivo/{id}` | Buscar por ID |
| GET | `/areas-cultivo/produtor/{id}` | Por produtor |
| POST | `/areas-cultivo` | Criar |
| PUT | `/areas-cultivo/{id}` | Atualizar |
| DELETE | `/areas-cultivo/{id}` | Deletar |

### Monitoramentos
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/monitoramentos` | Listar todos |
| GET | `/monitoramentos/{id}` | Buscar por ID |
| GET | `/monitoramentos/area/{id}` | Por área |
| POST | `/monitoramentos` | Criar |
| PUT | `/monitoramentos/{id}` | Atualizar |
| DELETE | `/monitoramentos/{id}` | Deletar |

### Alertas
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/alertas` | Listar todos |
| GET | `/alertas/{id}` | Buscar por ID |
| GET | `/alertas/area/{id}` | Por área |
| POST | `/alertas` | Criar |
| PUT | `/alertas/{id}` | Atualizar |
| DELETE | `/alertas/{id}` | Deletar |

---

## 🧪 Exemplo de Teste

### Criar produtor
```http
POST /produtores
Authorization: Bearer {token}
Content-Type: application/json

{
  "nome": "João Silva",
  "email": "joao@email.com",
  "cpf": "12345678901",
  "telefone": "11999999999",
  "cidade": "Ribeirão Preto",
  "estado": "SP"
}
```

### Criar área de cultivo
```http
POST /areas-cultivo
Authorization: Bearer {token}
Content-Type: application/json

{
  "nomeArea": "Setor A1",
  "cultura": "Soja",
  "latitude": -23.55,
  "longitude": -46.63,
  "hectares": 150.0,
  "produtorId": 1
}
```

### Criar monitoramento
```http
POST /monitoramentos
Authorization: Bearer {token}
Content-Type: application/json

{
  "indiceNdvi": 0.65,
  "ndviAnterior": 0.72,
  "umidadeSolo": 45.2,
  "temperaturaSolo": 28.5,
  "areaCultivoId": 1
}
```

### Criar alerta
```http
POST /alertas
Authorization: Bearer {token}
Content-Type: application/json

{
  "tipoAlerta": "ESTRESSE_HIDRICO",
  "observacao": "Queda de NDVI detectada",
  "areaCultivoId": 1
}
```

---

## 🌐 Swagger

Acesse a documentação completa em:
```
http://localhost:8080/swagger-ui.html
```

Clique em **Authorize**, cole o token JWT e teste todos os endpoints.
