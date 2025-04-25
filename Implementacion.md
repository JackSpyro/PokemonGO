# Guía de Despliegue en Azure Static Web Apps via GitHub Fork

## Prerrequisitos
- Cuenta de GitHub: [https://github.com](https://github.com)
- Cuenta de Microsoft Azure: [https://portal.azure.com](https://portal.azure.com) (el nivel Free es suficiente)
- Repositorio con sitio estático (HTML/CSS/JS o framework como React/Angular/Vue)

---

## Paso 1: Hacer Fork del repositorio
1. Navega al repositorio que deseas desplegar (ejemplo: [plantilla básica de Azure](https://github.com/Azure-Samples/js-e2e-static-web-app))
2. Haz clic en el botón "Fork" en la esquina superior derecha
3. Selecciona tu cuenta personal como destino del fork

---

## Paso 2: Crear recurso en Azure Portal
1. Inicia sesión en el [Portal de Azure](https://portal.azure.com)
2. En la barra de búsqueda, escribe "Static Web Apps" y selecciona el servicio
3. Haz clic en "Crear"
4. Completa la configuración básica:
   - **Suscripción**: Selecciona tu suscripción
   - **Grupo de recursos**: Crea uno nuevo o selecciona existente
   - **Nombre**: Asigna un nombre descriptivo (ej: `mi-app-estatica`)
   - **Región**: Selecciona la más cercana a tu ubicación

---

## Paso 3: Configurar conexión con GitHub
1. En la sección "Detalles de implementación":
   - Selecciona "GitHub" como origen
   - Haz clic en "Iniciar sesión con GitHub" y autoriza la conexión
2. Especifica los detalles del repositorio:
   - **Organización**: Tu cuenta personal
   - **Repositorio**: El que hiciste fork anteriormente
   - **Rama**: `main` o `master` (según tu repositorio)

---

## Paso 4: Configuración de compilación
Para un sitio básico (HTML/CSS puro):
```yaml
app_location: "/"
output_location: ""
api_location: ""
```
---
## Paso 5: Configurar seguridad con staticwebapp.config.json
Para agregar cabeceras de seguridad HTTP, crea un archivo en tu repositorio llamado:

staticwebapp.config.json

Coloca el siguiente contenido:
```yaml
{
    "globalHeaders": {
        "Content-Security-Policy": "default-src 'self'; img-src 'self' https://raw.githubusercontent.com https://pokeapi.co https://www.packages.org/publications/open-access.html",
        "X-Frame-Options": "DENY",
        "Permissions-Policy": "geolocation=(), microphone=(), camera=()"
    },
    "navigationFallback": {
        "rewrite": "/index.html",
        "exclude": ["/images/", "/css/", "/js/", "/favicon.ico"]
    }
}


