# 🛡️ AdGuard Home - Centro de Control Local

Este proyecto despliega una instancia de **AdGuard Home** configurada y lista para usar en tu equipo local mediante Docker.

---

## 🚀 Acceso al Panel de Control

El asistente de configuración inicial ya ha sido completado, por lo que el puerto 3000 ya no es necesario. El acceso se realiza directamente a través del panel de administración.

*   **URL**: [http://localhost:8081](http://localhost:8081)
*   **Usuario**: `izanmn`
*   **Contraseña**: `Asdqwe123`

---

## 🛠️ Configuración de Red

### 1. Puertos Activos
*   **Servicio DNS**: Puerto `53` (TCP/UDP) expuesto para resolver consultas.
*   **Panel Web**: Puerto `8081` (mapeado al puerto 80 interno).
*   **Seguridad**: Puertos `443` y `853` preparados para DNS cifrado (DoH/DoT).

### 2. DNS Upstream (Salida Segura)
El servidor utiliza **Quad9 (DNS-over-HTTPS)** para resolver tus consultas de forma privada y protegida contra malware:
*   `https://dns10.quad9.net/dns-query`

### 3. Configuración en este equipo (Windows)
Para que este PC use el AdGuard que acabas de desplegar, ejecuta este comando en **PowerShell (como Administrador)**:
```powershell
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses ("127.0.0.1")
```

---

## 🛡️ Filtros y Bloqueos Seleccionados

Se han activado las siguientes listas para un equilibrio perfecto entre bloqueo y estabilidad:
*   **OISD (Big)**: La lista "todo en uno" más recomendada.
*   **AdGuard DNS Filter**: Filtro base oficial de AdGuard.
*   **Steven Black's List**: Protección integral contra trackers.
*   **AWAvenue Ads Rule**: Bloqueo de anuncios en aplicaciones.

---

## 🛠️ Guía de Gestión de Bloqueos

### Cómo bloquear una web manualmente
Si quieres bloquear un dominio específico (ej. `youtube.com`):
1.  Ve a **Filtros** -> **Reglas de filtrado personalizadas**.
2.  Añade la línea: `||youtube.com^`
3.  Haz clic en **Aplicar**.

*Nota: No añadas dominios sueltos en la sección "Listas de bloqueo", ya que esa sección solo acepta URLs de archivos de texto (.txt).*

---

## 📂 Gestión del Proyecto
*   **Iniciar servicio**: `docker-compose up -d`
*   **Reiniciar**: `docker-compose restart adguardhome`
*   **Ver estadísticas en tiempo real**: `docker-compose logs -f`
