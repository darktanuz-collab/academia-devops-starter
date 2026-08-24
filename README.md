# Academia DevOps - Starter Repository

Bienvenido a **Academia DevOps**. Este es el repositorio de inicio para el bootcamp de DevOps enfocado en Salesforce.

## 📋 Requisitos Previos

Antes de empezar, asegúrate de tener instalado:

- **Git** - Control de versiones
  - Verifica: `git --version`
  - Instala desde: https://git-scm.com/

- **Visual Studio Code** - Editor de código
  - Descarga desde: https://code.visualstudio.com/

- **Salesforce CLI (SFDX)**
  - Verifica: `sfdx --version`
  - Instala desde: https://developer.salesforce.com/tools/sfdxcli

- **Salesforce Extension Pack** - Extensión de VS Code
  - Abre VS Code → Extensions → Busca "Salesforce Extension Pack" → Instala

- **Acceso a Dev Sandbox de Salesforce** - Tu organización de prueba

## 🚀 Quick Start

### 1. Clonar el Repositorio

```bash
git clone https://github.com/darktanuz-collab/academia-devops-starter.git
cd academia-devops-starter
```

### 2. Verificar Estructura

```bash
ls -la
# Deberías ver: force-app/, docs/, README.md, sfdx-project.json
```

### 3. Autenticarte en Salesforce

```bash
sfdx auth:web:login --alias mi-sandbox --instanceurl https://[tu-sandbox].salesforce.com
```

Reemplaza `[tu-sandbox]` con tu sandbox URL (ej: `testorg-dev.salesforce.com`)

### 4. Abrir en VS Code

```bash
code .
```

---

## 📚 Labs

Este repositorio contiene 5 labs prácticos para aprender DevOps con Salesforce:

| Lab | Tema | Duración | Descripción |
|-----|------|----------|-------------|
| **Lab 1** | Git Basics | 20 min | Clonar repo, crear rama, hacer commits |
| **Lab 2** | Move Changes (SFDX) | 20 min | Conectar a Salesforce, hacer cambios, deployar |
| **Lab 3** | Múltiples Ambientes | 15 min | Validar cambios en Dev y QA |
| **Lab 4** | Pull Request Workflow | 20 min | Code review, approval, merge |
| **Lab 5** | Release Simulation | 15 min | Tagging, versionado, rollback |

**Ver detalles:** [docs/LABS.md](docs/LABS.md)

---

## 🌳 Branch Strategy

Este repositorio usa **Git Flow**:

```
main (producción)
  ↑
  └── release/1.0 (rama de release)
       ↑
       └── develop (pre-producción)
            ↑
            ├── feature/tu-cambio-1
            ├── feature/tu-cambio-2
            └── feature/tu-cambio-3
```

**Reglas:**
- **NUNCA** hagas commit directo a `main` o `develop`
- Siempre crea una rama `feature/tu-nombre` desde `develop`
- Haz cambios en tu rama
- Abre un Pull Request (PR)
- Espera aprobación
- Mergea cuando esté aprobado

---

## 📝 Cómo Contribuir

### Paso 1: Crea tu Rama

```bash
git checkout develop
git pull origin develop
git checkout -b feature/tu-nombre
```

### Paso 2: Haz Cambios

Edita archivos en `force-app/` o `docs/`

```bash
# Ejemplo: Crear Apex Class
sfdx force:apex:class:create --classname MiClase --outputdir force-app/main/default/classes
```

### Paso 3: Commit los Cambios

```bash
git add .
git commit -m "feat: descripción de tu cambio"
# Ej: "feat: agregar HelloWorld Apex class"
```

### Paso 4: Push a GitHub

```bash
git push --set-upstream origin feature/tu-nombre
```

### Paso 5: Abre un Pull Request

1. Ve a https://github.com/darktanuz-collab/academia-devops-starter
2. Click "Compare & Pull Request"
3. Descripción clara de qué hiciste y por qué
4. Click "Create Pull Request"
5. **Espera aprobación**

### Paso 6: Mergea (una vez aprobado)

```bash
git checkout develop
git pull origin develop
git merge feature/tu-nombre
git push origin develop
```

---

## 🔐 Protected Branches

Las ramas `main` y `develop` están protegidas:

- ✅ Solo se pueden mergear vía Pull Request
- ✅ Requieren aprobación del instructor
- ✅ Las ramas se eliminan automáticamente después del merge

---

## 📂 Estructura del Repositorio

```
academia-devops-starter/
├── force-app/                    # Código Salesforce
│   └── main/
│       └── default/
│           ├── classes/          # Apex Classes (aquí creas las tuyas)
│           ├── triggers/         # Apex Triggers
│           └── objects/          # Objetos personalizados
├── docs/                         # Documentación
│   ├── LABS.md                   # Guía detallada de los 5 labs
│   └── cambios.md                # Archivo donde registran su avance
├── .gitignore                    # Archivos que Git ignora
├── sfdx-project.json             # Configuración de SFDX
└── README.md                     # Este archivo
```

---

## 🆘 Troubleshooting

### Error: "sfdx: command not found"

Salesforce CLI no está en tu PATH. Reinstala desde:
https://developer.salesforce.com/tools/sfdxcli

### Error: "No org configured"

No has autenticado tu org. Ejecuta:

```bash
sfdx auth:web:login --alias mi-sandbox --instanceurl https://[tu-sandbox].salesforce.com
```

### Error: "Permission denied" en Git

Configura tus credenciales de GitHub:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu.email@gmail.com"
```

### Error: "Merge conflict"

Si dos branches modifican el mismo archivo:

```bash
# Ver conflictos
git status

# Edita manualmente el archivo, resuelve conflictos
# Luego:
git add .
git commit -m "fix: resolver merge conflict"
git push
```

---

## 📞 Contacto

¿Preguntas? Abre un **Issue** en este repositorio o contacta al instructor.

---

## ⭐ Buena Suerte

Recuerda:
- **Small commits** (cambios pequeños y frecuentes)
- **Clear commit messages** (describe QUÉ y POR QUÉ)
- **Code review mindset** (escribe para que otros entiendan)
- **Test before pushing** (valida localmente primero)

¡Bienvenido a Academia DevOps! 🚀
