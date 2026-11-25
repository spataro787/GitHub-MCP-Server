# 🤖 GitHub MCP Server —

![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white)
![MCP SDK](https://img.shields.io/badge/MCP_SDK-8A2BE2?style=for-the-badge&logo=openai&logoColor=white)
![Zod](https://img.shields.io/badge/Zod-3E67B1?style=for-the-badge&logo=zod&logoColor=white)
![Octokit](https://img.shields.io/badge/Octokit-181717?style=for-the-badge&logo=github&logoColor=white)
![Vitest](https://img.shields.io/badge/Vitest-6E9F18?style=for-the-badge&logo=vitest&logoColor=white)

Servidor **MCP (Model Context Protocol)** desarrollado con **Node.js, TypeScript, Express, Zod y Octokit**, que permite a agentes de Inteligencia Artificial interactuar con GitHub mediante cinco herramientas (*Tools*) independientes, tipadas y validadas.

Utiliza el transporte **Streamable HTTP**, permitiendo la integración con clientes e inspectores MCP como MCP Inspector y Antigravity.

---

## 📌 Descripción del Proyecto

GitHub MCP Server funciona como intermediario entre un agente de Inteligencia Artificial y la API oficial de GitHub.

A través del protocolo MCP, expone herramientas que permiten ejecutar operaciones sobre repositorios, gestionar incidencias (*Issues*) y administrar archivos mediante instrucciones en lenguaje natural.

La implementación utiliza **Zod** para validar los datos de entrada y **Octokit** para comunicarse con la API de GitHub, manteniendo una arquitectura modular y organizada.

## 🛠️ Herramientas MCP Implementadas

| Herramienta | Descripción |
|---|---|
| `create_repository` | Crea repositorios públicos o privados. |
| `create_issue` | Registra nuevas incidencias (*Issues*) en un repositorio. |
| `list_repositories` | Lista los repositorios del usuario autenticado. |
| `create_commit` | Crea o actualiza archivos dentro de una rama mediante commits. |
| `list_issues` | Consulta incidencias según su estado: abiertas, cerradas o todas. |

## 🎯 Casos de Uso y Automatización

- **Automatización de repositorios:** creación de repositorios mediante instrucciones en lenguaje natural.
- **Gestión de Issues:** registro de tareas, errores y solicitudes de mejora.
- **Administración de archivos:** creación y actualización de archivos mediante commits.
- **Integración con agentes de IA:** permite que clientes compatibles con MCP interactúen con GitHub.
- **Validación de operaciones:** controla los datos de entrada mediante esquemas Zod.

## 🏗️ Arquitectura del Sistema

```text
┌─────────────────────────┐
│         Usuario         │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│  Cliente / Agente de IA │
│ Antigravity / Inspector │
└────────────┬────────────┘
             │ Streamable HTTP
             ▼
┌─────────────────────────┐
│    GitHub MCP Server    │
│     Node.js + Express   │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│       Zod Schemas       │
│   Validación de datos   │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│      MCP Tools Layer    │
│   5 herramientas Tools  │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│     Octokit Client      │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│        GitHub API       │
└─────────────────────────┘
```

## 📁 Estructura del Proyecto

```text
github-mcp-server/
├── src/
│   ├── app.ts                 # Servidor Express y endpoints HTTP
│   ├── mcp.ts                 # Definición y registro del servidor MCP
│   ├── types.ts               # Interfaces y tipos globales
│   ├── errors/                # Clases de errores personalizados
│   ├── github/                # Cliente Octokit y operaciones de GitHub
│   ├── schemas/               # Esquemas de validación Zod
│   ├── tools/                 # Implementación modular de las 5 Tools
│   └── utils/                 # Logger estructurado y retry pattern
├── tests/                     # Pruebas automatizadas con Vitest
├── server.ts                  # Punto de entrada principal
├── vitest.config.ts           # Configuración de Vitest
└── tsconfig.json              # Configuración de TypeScript
```

## 🧪 Pruebas Automatizadas

El proyecto incluye pruebas unitarias y de integración desarrolladas con **Vitest**, orientadas a verificar el funcionamiento de las herramientas, la validación de datos y la comunicación con GitHub.

### Suites de pruebas

- `schemas.test.ts`: validación de esquemas y datos de entrada con Zod.
- `tools.test.ts`: ejecución individual de las herramientas MCP.
- `github.test.ts`: pruebas del cliente Octokit y operaciones de GitHub.
- `mcp.integration.test.ts`: pruebas de integración del servidor MCP.

### Resultado de ejecución

```bash
npm test
```

```text
✓ tests/schemas.test.ts
✓ tests/tools.test.ts
✓ tests/mcp.integration.test.ts
✓ tests/github.test.ts

Test Files  4 passed (4)
Tests      17 passed (17)
```

**Resultado: 17 pruebas aprobadas.**

## ⚙️ Instalación y Configuración Local

### 1. Clonar el repositorio

```bash
git clone https://github.com/spataro787/Proyecto-M5--Agustin-Spataro.git
cd Proyecto-M5--Agustin-Spataro
```

### 2. Instalar dependencias

```bash
npm install
```

### 3. Configurar variables de entorno

Crear un archivo `.env` a partir de `.env.example` y configurar las credenciales:

```env
GITHUB_TOKEN=tu_personal_access_token
PORT=3000
```

El token de GitHub debe contar con los permisos necesarios para las operaciones que se desean realizar.

**Importante:** nunca publiques tu token ni compartas credenciales privadas.

### 4. Compilar y ejecutar

```bash
npm run build
npm start
```

## 🧰 Tecnologías Utilizadas

- **Node.js:** entorno de ejecución del servidor.
- **TypeScript:** tipado estático y organización del código.
- **Express:** gestión de endpoints HTTP.
- **Model Context Protocol (MCP):** comunicación entre agentes de IA y herramientas externas.
- **Zod:** validación de datos y esquemas.
- **Octokit:** integración con la API oficial de GitHub.
- **Vitest:** pruebas automatizadas.
- **Streamable HTTP:** transporte para la comunicación MCP.

## 👨‍💻 Autor

**Agustín Spataro**  
Backend & Full Stack Developer

- 🌐 Portfolio: https://agustin-spataro.vercel.app/
- 💼 LinkedIn: https://linkedin.com/in/agustin-spataro-dev
- 🐙 GitHub: https://github.com/spataro787

---

Desarrollado con foco en **arquitectura modular, integración de Inteligencia Artificial, automatización de procesos y buenas prácticas de desarrollo Backend**.
