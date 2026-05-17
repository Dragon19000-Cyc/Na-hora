<div align="center">

# 📱 NaHora

**Plataforma de agendamento de serviços locais**

Conecte clientes a profissionais autônomos de forma rápida e simples.

![Node.js](https://img.shields.io/badge/Node.js-18%2B-green?style=flat-square&logo=node.js)
![React Native](https://img.shields.io/badge/React%20Native-Expo-blue?style=flat-square&logo=expo)
![SQLite](https://img.shields.io/badge/Banco-SQLite-lightgrey?style=flat-square&logo=sqlite)
![TypeScript](https://img.shields.io/badge/TypeScript-5.x-blue?style=flat-square&logo=typescript)

</div>

---

## 🧠 Como o projeto funciona

O **NaHora** é dividido em dois módulos que trabalham juntos:

```
NaHora/
├── Backend/     → API REST em Node.js + Express + SQLite
└── Frontend/    → App mobile em React Native (Expo)
```

### Fluxo principal

```
Cliente abre o app
    → Visualiza profissionais disponíveis
    → Escolhe um serviço
    → Seleciona data e horário
    → Confirma o agendamento ✅

Empreendedor (profissional)
    → Cadastra seus serviços
    → Vê agenda do dia
    → Confirma / Conclui / Cancela atendimentos
```

### Dois perfis de usuário

| Perfil | Funcionalidades |
|---|---|
| **Cliente** | Buscar profissionais, agendar serviços, ver histórico, notificações |
| **Empreendedor** | Dashboard com métricas, agenda semanal, gerenciar serviços, perfil público |

---

## 🛠️ Tecnologias

### Backend
- **Node.js** + **Express** — servidor HTTP
- **SQLite** via `sqlite3` — banco de dados local
- **JWT** (`jsonwebtoken`) — autenticação stateless
- **bcryptjs** — hash de senhas

### Frontend
- **React Native** + **Expo Router** — app mobile com navegação por arquivo
- **TypeScript** — tipagem estática
- **Axios** — cliente HTTP com interceptor de token
- **AsyncStorage** — persistência do JWT no dispositivo
- **expo-linear-gradient**, **@expo/vector-icons** — UI

---

## ⚙️ Como rodar localmente

### Pré-requisitos

- [Node.js 18+](https://nodejs.org)
- [npm](https://npmjs.com)
- [Expo Go](https://expo.dev/go) no celular (para testar no dispositivo físico)

---

### 1. Clone o repositório

```bash
git clone https://github.com/Macielv7/On-Time.git
cd On-Time
```

---

### 2. Configurar e rodar o Backend

```bash
cd Backend
npm install
```

Crie o arquivo `.env` na pasta `Backend/`:

```env
PORT=3000
JWT_SECRET=sua_chave_secreta_aqui
JWT_EXPIRES_IN=7d
NODE_ENV=development
DB_PATH=./nahora.db
```

Inicie o servidor:

```bash
npm start
```

O banco SQLite é criado automaticamente com todas as tabelas na primeira execução.

✅ API disponível em: `http://localhost:3000`

| Endpoint | Descrição |
|---|---|
| `GET /health` | Status da API |
| `POST /api/auth/register` | Cadastro |
| `POST /api/auth/login` | Login |
| `GET /api/professionals` | Listar profissionais |
| `GET /api/services` | Listar serviços |
| `POST /api/appointments` | Criar agendamento |
| `GET /api/notifications` | Notificações do usuário |

---

### 3. Configurar e rodar o Frontend

Em outro terminal:

```bash
cd Frontend
npm install
npm start
```

O Expo abrirá um QR Code no terminal.

- **Celular físico**: abra o app **Expo Go** e escaneie o QR Code
- **Navegador**: pressione `W` para abrir no browser (web)
- **Emulador Android**: pressione `A`
- **Simulador iOS**: pressione `I` (somente macOS)

> ⚠️ **Importante**: se estiver testando em dispositivo físico, edite `Frontend/services/api.ts` e troque `localhost` pelo IP da sua máquina na rede local:
> ```ts
> export const API_URL = 'http://192.168.x.x:3000'; // seu IP local
> ```

---

## 🗂️ Estrutura do projeto

```
NaHora/
├── Backend/
│   ├── src/
│   │   ├── database/
│   │   │   ├── connection.js      # Conexão SQLite
│   │   │   └── migrations.js      # Criação das tabelas
│   │   ├── middleware/
│   │   │   └── auth.js            # Validação do JWT
│   │   ├── modules/
│   │   │   ├── auth/              # Login e cadastro
│   │   │   ├── professionals/     # Profissionais e categorias
│   │   │   ├── services/          # Serviços dos profissionais
│   │   │   ├── appointments/      # Agendamentos
│   │   │   └── notifications/     # Notificações
│   │   └── index.js              # Ponto de entrada da API
│   ├── .env                       # ⚠️ Não commitado (criar manualmente)
│   └── package.json
│
└── Frontend/
    ├── app/
    │   ├── (auth)/               # Login e cadastro
    │   ├── (client)/             # Área do cliente
    │   │   ├── home.tsx          # Tela inicial com busca
    │   │   ├── professional/     # Detalhes do profissional
    │   │   ├── booking.tsx       # Fluxo de agendamento
    │   │   └── appointments.tsx  # Meus agendamentos
    │   ├── (entrepreneur)/       # Área do empreendedor
    │   │   ├── dashboard.tsx     # Painel com métricas
    │   │   ├── agenda.tsx        # Agenda semanal
    │   │   ├── services.tsx      # Gerenciar serviços
    │   │   └── profile.tsx       # Perfil público
    │   └── notifications.tsx     # Notificações
    ├── services/                 # Clients da API (Axios)
    ├── contexts/                 # AuthContext (estado global)
    └── constants/                # Tema visual (cores, espaçamentos)
```

---

## 👤 Usuários de teste

Após rodar o backend, cadastre usuários pelo app ou pela API. Exemplo rápido:

```bash
# Registrar um cliente
curl -X POST http://localhost:3000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"name":"João Silva","email":"joao@email.com","password":"123456","role":"client"}'

# Registrar um empreendedor
curl -X POST http://localhost:3000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"name":"Carlos Mendes","email":"carlos@email.com","password":"123456","role":"entrepreneur"}'
```

---

## 📄 Licença

MIT © 2025 — NaHora
