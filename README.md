# AdGuard Home - Documentación del Proyecto

Este repositorio contiene la configuración y el despliegue de **AdGuard Home** utilizando Docker, diseñado para proporcionar un control total sobre el tráfico de red, bloqueo de publicidad y protección de privacidad a nivel de DNS.

---

## 🚀 Proceso de Instalación y Despliegue

El despliegue se ha realizado mediante **Docker Compose**, lo que garantiza un entorno aislado y fácil de mantener.

### Requisitos Previos
*   Docker y Docker Compose instalados.
*   Puertos necesarios libres (especialmente el puerto 53 para DNS).

### Pasos de Instalación
1.  **Clonación/Preparación**: Asegúrate de que el archivo `docker-compose.yml` esté en el directorio del proyecto.
2.  **Levantamiento del servicio**: Ejecuta el siguiente comando en la terminal:
    ```bash
    docker-compose up -d
    ```
3.  **Configuración Inicial**: Accede a `http://localhost:3000` para completar el asistente de configuración de AdGuard por primera vez.

---

## 🛠️ Configuración de Red

La configuración de red está optimizada para la seguridad y el rendimiento:

### Puertos Mapeados
*   **DNS (53 TCP/UDP)**: Tráfico DNS estándar.
*   **Panel de Administración (8081)**: Acceso a la interfaz web (mapeado al puerto 80 del contenedor).
*   **HTTPS/DoH (443)**: DNS sobre HTTPS.
*   **DoT (853)**: DNS sobre TLS.
*   **Asistente (3000)**: Solo necesario para la instalación inicial.

### DNS Upstream (Servidores de Salida)
Se ha configurado **Quad9** como proveedor principal mediante el protocolo seguro **DNS-over-HTTPS (DoH)**:
*   `https://dns10.quad9.net/dns-query`

**Ventajas**: Quad9 ofrece protección contra malware y phishing integrada, y el uso de DoH asegura que tus consultas DNS estén cifradas y no puedan ser interceptadas por el ISP.

---

## 🛡️ Listas de Bloqueo Seleccionadas

Se han seleccionado cuidadosamente varias listas para maximizar el bloqueo sin romper la experiencia de navegación:

1.  **AdGuard DNS filter**: La lista base oficial de AdGuard, optimizada para evitar publicidad intrusiva.
2.  **AdGuard DNS Popup Hosts**: Especializada en bloquear ventanas emergentes (popups) molestas.
3.  **AWAvenue Ads Rule**: Una lista potente que complementa el bloqueo de anuncios en aplicaciones y webs específicas.
4.  **Dan Pollock's List**: Una de las listas más veteranas y fiables para bloquear hosts maliciosos y de publicidad.
5.  **Steven Black's List**: Una lista consolidada que combina múltiples fuentes para un bloqueo integral de trackers y malware.

*Nota: Se ha añadido una regla personalizada para `twitch.tv` según los requerimientos del usuario.*

---

## 📖 Cómo Usar

### 1. Acceso al Panel
Entra en la interfaz web para ver estadísticas y gestionar filtros:
*   **URL**: `http://<IP-DE-TU-SERVIDOR>:8081`

### 2. Configuración en Dispositivos
Para que los dispositivos de tu red utilicen este AdGuard, debes cambiar su servidor DNS:
*   **IPv4**: Usa la dirección IP de la máquina donde corre Docker.
*   **Recomendación**: Configura la IP del servidor AdGuard directamente en tu router para que todos los dispositivos de la casa estén protegidos automáticamente.

### 3. Comandos Útiles
*   **Ver logs**: `docker-compose logs -f`
*   **Reiniciar**: `docker-compose restart`
*   **Actualizar imagen**: `docker-compose pull && docker-compose up -d`

---

## 📂 Estructura de Archivos
*   `docker-compose.yml`: Definición del contenedor y puertos.
*   `confdir/`: Directorio persistente para la configuración (`AdGuardHome.yaml`).
*   `workdir/`: Directorio persistente para datos de trabajo y bases de datos de estadísticas.
