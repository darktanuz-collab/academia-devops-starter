# 🧪 Academia DevOps - Guía Detallada de Labs

Esta es la guía paso-a-paso para los **5 labs prácticos** del bootcamp DevOps.

**Duración total:** 90 minutos (sin break)

---

## LAB 1: Git Basics (20 min)

### Objetivo
Entender los conceptos fundamentales de Git: clonar, ramas, commits.

### Pasos

#### 1.1 Abrir Terminal en VS Code

- Abre VS Code
- Presiona `Ctrl + ~` para abrir la terminal integrada
- Verifica que estés en un directorio limpio:

```powershell
cd ~
```

#### 1.2 Clonar el Repositorio

```powershell
git clone https://github.com/darktanuz-collab/academia-devops-starter.git
cd academia-devops-starter
```

**Esperado:** Ves la carpeta `academia-devops-starter` con archivos dentro.

#### 1.3 Explorar el Historial de Git

```powershell
git log --oneline
```

**Qué ves:** Lista de commits anteriores en el repo.

```powershell
git branch -a
```

**Qué ves:** Ramas disponibles (`main`, `develop`)

#### 1.4 Crear Tu Propia Rama

```powershell
git checkout -b feature/mi-primer-cambio
```

Reemplaza `mi-primer-cambio` con tu nombre (ej: `feature/gabriel-lab1`)

```powershell
git branch
```

**Qué ves:** Tu rama nueva aparece con un `*` al lado (indicando que estás en ella)

#### 1.5 Hacer Un Cambio

- Abre el archivo `docs/cambios.md` en VS Code
- Agrega una línea con tu nombre:

```
- [Tu Nombre] - Lab 1 completado - [Fecha]
```

Ejemplo:
```
- Gabriel Aguilar - Lab 1 completado - 2026-08-24
```

- Guarda el archivo (`Ctrl + S`)

#### 1.6 Git Commit

```powershell
git status
```

**Qué ves:** El archivo `docs/cambios.md` aparece como modificado (rojo)

```powershell
git add .
```

**Qué ves:** Nada, pero el cambio está "staged"

```powershell
git status
```

**Qué ves:** Ahora `docs/cambios.md` aparece en verde (staged)

```powershell
git commit -m "feat: agregar mi nombre a cambios.md - Lab 1"
```

**Qué ves:** Confirmación del commit con un hash (ej: `abc1234`)

#### 1.7 Ver Tu Commit

```powershell
git log --oneline
```

**Qué ves:** Tu commit aparece en la parte superior de la lista

```powershell
git show HEAD
```

**Qué ves:** Detalles completos de tu commit (quién, cuándo, qué cambió)

---

### ✅ Checkpoint Lab 1

Verifica que completaste:
- ✓ Clonaste el repo
- ✓ Estás en tu rama `feature/tu-nombre`
- ✓ Hiciste un cambio en `docs/cambios.md`
- ✓ Committeaste el cambio
- ✓ Ves tu commit en `git log`

**Si todo está ✓, Lab 1 COMPLETADO**

---

## LAB 2: Move Changes in Salesforce (20 min)

### Objetivo
Conectar VS Code a tu Salesforce Dev sandbox, hacer cambios y deployarlos vía SFDX.

### Requisitos
- Acceso a tu Dev sandbox de Salesforce
- SFDX instalado (`sfdx --version`)
- Salesforce Extension Pack en VS Code

### Pasos

#### 2.1 Autenticarte en Salesforce

```powershell
sfdx auth:web:login --alias mi-sandbox --instanceurl https://[TU-SANDBOX].salesforce.com
```

Reemplaza `[TU-SANDBOX]` con tu sandbox URL (ej: `testorg-dev`)

**Qué pasa:**
- Se abre un navegador
- Logeas con tu usuario de Salesforce
- Das permisos
- Se cierra automáticamente y vuelves a terminal

```powershell
sfdx force:org:list
```

**Qué ves:** Tu org aparece en la lista, con un `*` si es la default

#### 2.2 Pullear Metadatos de tu Org

```powershell
sfdx force:source:pull --targetusername mi-sandbox
```

**Qué pasa:** Descarga la configuración actual de tu sandbox a la carpeta `force-app/`

**Qué ves:** Terminal muestra archivos sincronizados

```powershell
ls force-app/main/default/
```

**Qué ves:** Carpetas como `classes/`, `objects/`, etc.

#### 2.3 Crear Tu Primera Apex Class

En VS Code:
- Click derecho en la carpeta `force-app/main/default/classes/`
- Opción: "SFDX: Create Apex Class"
- Nombre: `HelloWorld` (reemplaza "HelloWorld" con tu nombre si prefieres)
- Enter

**Resultado:** Se crea archivo `HelloWorld.cls`

Edita el contenido a esto:

```apex
public class HelloWorld {
    public static String sayHello() {
        return 'Hello from ' + [SELECT Name FROM Organization LIMIT 1].Name;
    }
}
```

Guarda (`Ctrl + S`)

#### 2.4 Deployar a tu Sandbox

```powershell
sfdx force:source:push --targetusername mi-sandbox
```

**Qué pasa:** Tu código se sube a Salesforce (sin UI manual)

**Qué ves:** Confirmación de éxito

#### 2.5 Verificar en Salesforce (Opcional)

- Abre tu org de Salesforce en navegador
- Ve a Developer Console (`Ctrl + K` en la org)
- Ve a "Apex Classes"
- Busca `HelloWorld`
- Deberías ver tu código ahí

#### 2.6 Trackearlo en Git

```powershell
git status
```

**Qué ves:** Cambios nuevos en `force-app/`

```powershell
git add force-app/
git commit -m "feat: agregar HelloWorld Apex class - Lab 2"
```

```powershell
git log --oneline
```

**Qué ves:** Tu nuevo commit

---

### ✅ Checkpoint Lab 2

Verifica que completaste:
- ✓ Autenticado en Salesforce vía SFDX
- ✓ Creaste Apex class `HelloWorld`
- ✓ Deployaste a tu sandbox vía `force:source:push`
- ✓ Ves el código en tu org de Salesforce
- ✓ Committeaste los cambios en Git

**Si todo está ✓, Lab 2 COMPLETADO**

---

## LAB 3: Múltiples Ambientes (15 min)

### Objetivo
Entender cómo cambios fluyen de Dev → QA → Prod. Aprender a revertir cambios.

### Requisitos
- Lab 2 completado
- Acceso a un QA sandbox (usa el mismo si no tienes otro)

### Pasos

#### 3.1 Conectarte al QA Sandbox

```powershell
sfdx auth:web:login --alias mi-qa --instanceurl https://[TU-QA-SANDBOX].salesforce.com
```

Si solo tienes 1 sandbox, usa el mismo:

```powershell
sfdx auth:web:login --alias mi-qa --instanceurl https://[TU-SANDBOX].salesforce.com
```

#### 3.2 Deployar a QA

```powershell
sfdx force:source:push --targetusername mi-qa
```

**Qué pasa:** El mismo código que está en Dev, ahora está en QA

#### 3.3 Verificar en Ambos

```powershell
sfdx force:org:list
```

**Qué ves:** Dos orgs conectadas

- Abre tu Dev sandbox → Developer Console → Apex Classes → `HelloWorld` ✓
- Abre tu QA sandbox → Developer Console → Apex Classes → `HelloWorld` ✓

**Concepto:** Mismo código, dos ambientes. Esto es **Environment Strategy**.

#### 3.4 Simular un Error en Dev

Edita `HelloWorld.cls` e introduce un "error" a propósito:

```apex
public class HelloWorld {
    public static String sayHello() {
        return 'BUG VERSION!';  // Propósito: simular error
    }
}
```

Guarda y deploya a Dev:

```powershell
sfdx force:source:push --targetusername mi-sandbox
```

**Resultado:** Dev tiene el "bug", pero QA sigue teniendo la versión anterior.

#### 3.5 Revertir en Dev

```powershell
git log --oneline
```

**Qué ves:** Tu historia de commits

```powershell
git checkout HEAD~1 -- force-app/
```

**Qué pasa:** Vuelves el archivo `HelloWorld.cls` a la versión anterior

```powershell
sfdx force:source:push --targetusername mi-sandbox
```

**Resultado:** Dev vuelve a tener la versión correcta (sin "bug")

- Abre tu Dev sandbox → Developer Console → `HelloWorld` → Debe mostrar "Hello from..." (sin "BUG")

**Concepto:** Con Git, revertir cambios es tan fácil como un comando.

#### 3.6 Commitear la "reversión"

```powershell
git status
```

```powershell
git add .
git commit -m "revert: quitar bug de HelloWorld - Lab 3"
```

---

### ✅ Checkpoint Lab 3

Verifica que completaste:
- ✓ Conectado a 2 orgs (Dev + QA)
- ✓ Deployaste el mismo código a ambas
- ✓ Ambas orgs tienen `HelloWorld`
- ✓ Simulaste un bug y lo revertiste con Git
- ✓ Committeaste todo en Git

**Si todo está ✓, Lab 3 COMPLETADO**

---

## LAB 4: Pull Request Workflow (20 min)

### Objetivo
Aprender el flujo de **code review**: crear PR, recibir aprobación, mergear.

### Pasos

#### 4.1 Pushear tu Rama a GitHub

```powershell
git push --set-upstream origin feature/[tu-nombre]
```

Reemplaza `[tu-nombre]` con tu nombre de rama (ej: `feature/gabriel-lab1`)

**Qué pasa:** Tu rama local se sube a GitHub

**Qué ves:** Confirmación de éxito

#### 4.2 Crear Pull Request en GitHub

1. Ve a https://github.com/darktanuz-collab/academia-devops-starter
2. Deberías ver un banner: "Compare & Pull Request"
3. Click en ese botón
4. Llena el PR:

**Título:**
```
feat: mis cambios de Lab 1-3
```

**Descripción:**
```markdown
## Qué hago
- Agregué mi nombre a cambios.md (Lab 1)
- Creé clase HelloWorld (Lab 2)
- Probé con múltiples ambientes (Lab 3)

## Por qué
Para practicar el workflow DevOps en Salesforce.

## Testing
- ✓ Git workflow completado
- ✓ Apex class deployada
- ✓ Multi-env validado
```

5. Click "Create Pull Request"

**Resultado:** Tu PR está abierto, esperando review

#### 4.3 Simular Code Review

Para este lab, el instructor (o un compañero) revisará:

1. Va a tu PR
2. Click "Files changed"
3. Review el código
4. Click "Review changes"
5. "Approve"

**Concepto:** Un segundo par de ojos valida tu código.

#### 4.4 Mergear el PR

Una vez aprobado:

1. Click "Merge pull request"
2. Click "Confirm merge"
3. Click "Delete branch" (limpiar)

**Resultado:** Tu código está ahora en `develop`

#### 4.5 Sincronizar Local

```powershell
git checkout develop
git pull origin develop
```

```powershell
git log --oneline
```

**Qué ves:** Tu commit aparece en develop

---

### ✅ Checkpoint Lab 4

Verifica que completaste:
- ✓ Push de rama a GitHub
- ✓ PR creado y aprobado
- ✓ Código mergeado a develop
- ✓ Local sincronizado con develop

**Si todo está ✓, Lab 4 COMPLETADO**

---

## LAB 5: Release Simulation (15 min)

### Objetivo
Entender **versionado**, **release tagging**, y **rollback**.

### Pasos

#### 5.1 Crear Release Branch

```powershell
git checkout -b release/1.0 develop
```

**Qué pasa:** Creas una rama `release/1.0` basada en `develop`

**Concepto:** Esta rama es el "congelado" del código para la versión 1.0. Cambios críticos solo.

#### 5.2 Etiquetar la Release

```powershell
git tag -a v1.0 -m "Release 1.0: First DevOps training release"
```

**Qué pasa:** Creas un "punto de guardado" en Git para la versión 1.0

```powershell
git push origin release/1.0
git push origin v1.0
```

**Qué ves:** Ambos, rama y tag, suben a GitHub

#### 5.3 Verificar en GitHub

1. Ve a https://github.com/darktanuz-collab/academia-devops-starter
2. Click en la pestaña "Releases"
3. Deberías ver `v1.0` listed

**Concepto:** Este tag es como un "punto de guardado" en un videojuego.

#### 5.4 Simular Rollback (Revertir a Versión Anterior)

Si algo sale mal en producción, puedes revertir:

```powershell
git log --oneline --all
```

Busca el commit anterior a tu release. Luego:

```powershell
git checkout v1.0 -- force-app/
```

**Qué pasa:** Los archivos en `force-app/` vuelven a la versión de `v1.0`

```powershell
sfdx force:source:push --targetusername mi-sandbox
```

**Qué pasa:** Deployas la versión vieja a tu sandbox (simulando un rollback a prod)

**Concepto:** En 2 comandos, revertiste todo. Eso es el poder de DevOps.

#### 5.5 Limpiar

Vuelve a develop:

```powershell
git checkout develop
git pull origin develop
```

---

### ✅ Checkpoint Lab 5

Verifica que completaste:
- ✓ Creaste rama release/1.0
- ✓ Etiquetaste como v1.0
- ✓ Tag visible en GitHub Releases
- ✓ Simulaste rollback
- ✓ Entiendes cómo revertir si es necesario

**Si todo está ✓, Lab 5 COMPLETADO**

---

## 🎉 ¡Completaste Academia DevOps!

Has aprendido:
✓ Git fundamentals (branches, commits, logs)
✓ Move changes con SFDX (pull, push, deploy)
✓ Multi-environment strategy (Dev, QA, Prod)
✓ Pull Request workflow (review, approval, merge)
✓ Release management (tagging, versioning, rollback)

**Próximos pasos:**
1. Practicar con cambios reales en tu org
2. Aprender CI/CD (automatización de pipelines)
3. Implementar testing automatizado
4. Escalar a equipos más grandes

---

## 📞 Troubleshooting Rápido

| Problema | Solución |
|----------|----------|
| "fatal: not a git repository" | Estás fuera de la carpeta. Haz `cd academia-devops-starter` |
| "sfdx: command not found" | SFDX no instalado. Ve a https://developer.salesforce.com/tools/sfdxcli |
| "Permission denied on GitHub" | Configura credenciales: `git config --global user.name "Tu Nombre"` |
| "Merge conflict" | Abre el archivo, resuelve manual, `git add`, `git commit` |
| "Can't authenticate in Salesforce" | Verifica URL sandbox y credenciales correctas |

---

¡Éxito! 🚀
