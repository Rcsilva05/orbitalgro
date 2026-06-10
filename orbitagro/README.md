# 🌱 OrbitAgro

> Monitoramento Agrícola via Satélite e IoT — FIAP Global Solution 2026/1

OrbitAgro antecipa riscos agrícolas combinando imagens de satélite, índice NDVI e sensores IoT para que produtores rurais tomem decisões **antes** da perda da produção.

---

## 👥 Integrantes

| Nome | RM | Turma |
|------|----|-------|
| Rodrigo Silva | RM565162 | 2TDSR |
| Nickolas Davi | RM564105 | 2TDSR |
| Samara Vilela | RM566133 | 2TDSR |
| Natália Cristina | RM564099 | 2TDSR |
| Otávio Ferreira | RM565960 | 2TDSR |

---

## 🔗 Links

| Item | Link |
|------|------|
| 🚀 Deploy | https://orbitalgro-production.up.railway.app |
| 📖 Swagger UI | https://orbitalgro-production.up.railway.app/swagger-ui/index.html |
| 📄 API Docs | https://orbitalgro-production.up.railway.app/api-docs |
| 📹 Vídeo de Apresentação | https://studio.youtube.com/video/enS0IGj6Yos/edit |
| 🎯 Vídeo Pitch | https://youtu.be/Jsow2t7mAt4  |
| 💻 Repositório | https://github.com/Rcsilva05/orbitalgro |

---

## 💡 Sobre o Projeto

Produtores rurais tomam decisões importantes tarde demais. Quando percebem visualmente seca, excesso de chuva, estresse hídrico ou perda de vigor da vegetação, parte da perda financeira já aconteceu.

O **OrbitAgro** antecipa esses riscos utilizando:
- Imagens de satélite e índice NDVI
- Sensores IoT (umidade e temperatura do solo)
- Alertas inteligentes automáticos

Permitindo decisões **preventivas** antes da perda da produção.

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

| Tecnologia | Versão | Uso |
|-----------|--------|-----|
| Java | 17 | Linguagem principal |
| Spring Boot | 3.2.5 | Framework |
| Spring Data JPA | 3.2.5 | Persistência |
| Spring Security | 6.2.4 | Autenticação |
| Spring HATEOAS | 2.2.2 | Hipermídia |
| Spring Validation | 3.2.5 | Validações |
| JWT (jjwt) | 0.11.5 | Tokens |
| Lombok | 1.18.32 | Produtividade |
| H2 Database | 2.2.224 | Banco em memória |
| Swagger/OpenAPI | 2.3.0 | Documentação |
| Maven | 3.8+ | Build |

---

## ▶️ Como Executar Localmente

### Pré-requisitos
- Java 17+
- Maven 3.8+
- IntelliJ IDEA (recomendado)

### Passo a passo

```bash
# 1. Clonar o repositório
git clone https://github.com/Rcsilva05/orbitalgro.git

# 2. Entrar na pasta do projeto
cd orbitalgro/orbitagro

# 3. Rodar o projeto
./mvnw spring-boot:run
```

A API estará disponível em: `http://localhost:8080`

Swagger local: `http://localhost:8080/swagger-ui/index.html`

---

## 🔐 Como Testar a API

### Passo 1 — Registrar usuário
```http
POST /auth/register
Content-Type: application/json

{
  "username": "admin",
  "password": "123456",
  "role": "ADMIN"
}
```

### Passo 2 — Fazer login e pegar o token
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

### Passo 3 — Autorizar no Swagger
```
Acessa o Swagger → clica em "Authorize" → cola o token → clica "Authorize"
```

### Passo 4 — Testar os endpoints

**Criar produtor:**
```http
POST /produtores
Authorization: Bearer {token}

{
  "nome": "João Silva",
  "email": "joao@email.com",
  "cpf": "12345678901",
  "telefone": "11999999999",
  "cidade": "Ribeirão Preto",
  "estado": "SP"
}
```

**Criar área de cultivo:**
```http
POST /areas-cultivo
Authorization: Bearer {token}

{
  "nomeArea": "Setor A1",
  "cultura": "Soja",
  "latitude": -23.55,
  "longitude": -46.63,
  "hectares": 150.0,
  "produtorId": 1
}
```

**Criar monitoramento:**
```http
POST /monitoramentos
Authorization: Bearer {token}

{
  "indiceNdvi": 0.65,
  "ndviAnterior": 0.72,
  "umidadeSolo": 45.2,
  "temperaturaSolo": 28.5,
  "areaCultivoId": 1
}
```

**Criar alerta:**
```http
POST /alertas
Authorization: Bearer {token}

{
  "tipoAlerta": "ESTRESSE_HIDRICO",
  "observacao": "Queda de NDVI detectada",
  "areaCultivoId": 1
}
```

---

## 📡 Endpoints Disponíveis

### Autenticação (público)
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| POST | `/auth/register` | Registrar usuário |
| POST | `/auth/login` | Login e obter token JWT |

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
| GET | `/areas-cultivo/produtor/{id}` | Listar por produtor |
| POST | `/areas-cultivo` | Criar |
| PUT | `/areas-cultivo/{id}` | Atualizar |
| DELETE | `/areas-cultivo/{id}` | Deletar |

### Monitoramentos
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/monitoramentos` | Listar todos |
| GET | `/monitoramentos/{id}` | Buscar por ID |
| GET | `/monitoramentos/area/{id}` | Listar por área |
| POST | `/monitoramentos` | Criar |
| PUT | `/monitoramentos/{id}` | Atualizar |
| DELETE | `/monitoramentos/{id}` | Deletar |

### Alertas
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/alertas` | Listar todos |
| GET | `/alertas/{id}` | Buscar por ID |
| GET | `/alertas/area/{id}` | Listar por área |
| POST | `/alertas` | Criar |
| PUT | `/alertas/{id}` | Atualizar |
| DELETE | `/alertas/{id}` | Deletar |

---

## 🎥 Vídeos

### Vídeo de Apresentação (até 10 minutos)
> 🔗 https://www.youtube.com/watch?v=enS0IGj6Yos

### Vídeo Pitch (até 3 minutos)
> 🔗 https://www.youtube.com/watch?v=Jsow2t7mAt4

---

## 📋 Checklist de Entrega

- [x] API REST com Spring Boot
- [x] CRUD completo das 4 entidades
- [x] Spring Security + JWT
- [x] HATEOAS nos endpoints
- [x] Spring Validation
- [x] DTOs com Java Records
- [x] Tratamento de exceções
- [x] Modelagem avançada (Embedded, herança)
- [x] Swagger/OpenAPI documentado
- [x] Deploy público no Railway
- [x] README completo
- [ ] Vídeo de apresentação
- [ ] Vídeo pitch
