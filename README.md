# OrbitAgro — API de monitoramento agrícola

API acadêmica para organizar produtores, áreas de cultivo, registros de monitoramento e alertas. O projeto também inclui autenticação com JWT e documentação interativa da API.

## Tecnologias

- Java 17 e Spring Boot 3.2.5
- Spring Web, Spring Data JPA e Spring HATEOAS
- Validação, autenticação JWT e Swagger/OpenAPI
- H2 em memória para desenvolvimento

## Executar localmente

Pré-requisitos: JDK 17 ou superior e Maven.

```bash
cd orbitagro
mvn spring-boot:run
```

A aplicação inicia em `http://localhost:8080`. A documentação interativa fica em [`http://localhost:8080/swagger-ui.html`](http://localhost:8080/swagger-ui.html).

O perfil atual usa H2 em memória; os dados são recriados quando a aplicação reinicia.

## Recursos disponíveis

- Autenticação: `/auth/login` e `/auth/register`
- Produtores: `/produtores`
- Áreas de cultivo: `/areas-cultivo`
- Monitoramentos: `/monitoramentos`
- Alertas: `/alertas`

Os recursos de produtores, áreas, monitoramentos e alertas oferecem operações de consulta e manutenção descritas no Swagger.