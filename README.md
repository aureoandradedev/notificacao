# 📧 Notificacao - Microsservico de Email

Microsservico de notificacoes por email desenvolvido com Java 17 e Spring Boot 3, utilizando Thymeleaf para templates HTML e JavaMailSender para envio via SMTP.

---

## 🛠️ Tecnologias Utilizadas

- Java 17
- Spring Boot 3.3.5
- Spring Mail (JavaMailSender)
- Thymeleaf (templates HTML)
- Docker
- Lombok
- Gradle
- GitHub Actions (CI)

---

## 📋 Funcionalidades

- Receber dados de tarefa via endpoint REST
- Renderizar template HTML com dados da tarefa
- Enviar email formatado ao usuario da tarefa
- Tratamento de erros de envio com excecao customizada

---

## 🔑 Endpoints

| Metodo | Rota | Descricao |
|--------|------|-----------|
| `POST` | `/email` | Enviar notificacao por email |

### Exemplo de Request Body:

```json
{
  "id": "1",
  "nomeTarefa": "Reuniao de Sprint",
  "descricao": "Planning da sprint 15",
  "dataCriacao": "01-08-2025 10:00:00",
  "dataEvento": "05-08-2025 14:00:00",
  "emailUsuario": "usuario@email.com",
  "statusNotificacaoEnum": "PENDENTE"
}
```

---

## 📧 Template de Email

O email e renderizado com **Thymeleaf** utilizando um template HTML estilizado contendo:

- Nome da tarefa
- Data do evento
- Descricao da tarefa
- Layout responsivo com header e footer

---

## ⚙️ Configuracao SMTP

Configurado para Gmail SMTP (`smtp.gmail.com`):

- Porta: 587 (STARTTLS)
- Autenticacao habilitada
- Credenciais via variaveis de ambiente

> **Nota:** As credenciais SMTP devem ser configuradas via variaveis de ambiente ou perfil Spring externo.

---

## 🐳 Docker

- **Dockerfile** multi-stage (build com Gradle + runtime com Eclipse Temurin 17)
- Porta da aplicacao: **8082**

### Executar localmente:

```bash
docker build -t notificacao .
docker run -p 8082:8082 notificacao
```

---

## 📂 Estrutura do Projeto

```
src/main
┣ controller             → Endpoint REST (EmailController)
┣ business               → Servico de envio de email (EmailService)
┣ business/dto           → DTO de tarefas (TarefasDTO)
┣ business/enums         → Status de notificacao
┣ infrastructure
┃ ┗ exceptions           → Excecao customizada (EmailException)
┗ resources
  ┗ templates            → Template HTML do email (notificacao.html)
```

---

## 📦 Como Executar Localmente

1. Clonar o projeto
```bash
git clone https://github.com/aureoandradedev/notificacao.git
```

2. Entrar na pasta
```bash
cd notificacao
```

3. Configurar credenciais SMTP (application.yaml ou variaveis de ambiente)

4. Rodar a aplicacao
```bash
./gradlew bootRun
```

---

## 🏗️ Arquitetura

Este microsservico faz parte de um sistema distribuido:

```
BFF (porta 8083) → Notificacao (porta 8082) → SMTP (Gmail)
                 → Agendador de Tarefas (porta 8081)
                 → Usuario (porta 8080)
```

---

## 👨‍💻 Autor

**Aureo Andrade**

- GitHub: [aureoandradedev](https://github.com/aureoandradedev)
- LinkedIn: [aureoandrade](https://www.linkedin.com/in/aureoandrade/)
