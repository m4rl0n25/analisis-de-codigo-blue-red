# 🧠 Guía de Respuesta por Incidente

Este cuadro resume las **acciones inmediatas** ante la ejecución de un script malicioso tipo *keylogger + grabador de webcam + exfiltrador SMTP*.

---

## ⚠️ Acciones Inmediatas (Contención y Remediación)

| **#** | **Acción** | **Descripción / Comando sugerido** |
|:--:|:--|:--|
| 1️⃣ | **Desconectar  cable de_red** | 🔌 Desactiva Wi-Fi o desconecta cable Ethernet.<br>**Windows:** `netsh interface set interface "Wi-Fi" admin=disabled`<br>**Linux:** `nmcli networking off` |
| 2️⃣ | **Identificar procesos sospechosos** | 📋 Buscar procesos Python activos.<br>**Windows:** `tasklist /FI "IMAGENAME eq python.exe"`<br>**Linux:** `ps aux | grep -i python` |
| 3️⃣ | **Finalizar proceso malicioso** | 💀 Terminar PID correspondiente.<br>**Windows:** `taskkill /PID <PID> /F`<br>**Linux:** `kill -9 <PID>` |
| 4️⃣ | **Eliminar artefactos** | 🗑️ Borrar carpetas creadas (`Data_Video`, `Data_Archivo_txt`).<br>**Windows:** `Remove-Item -Recurse -Force "$env:USERPROFILE\Data_Video"`<br>**Linux:** `rm -rf ~/Data_Video ~/Data_Archivo_txt` |
| 5️⃣ | **Cambiar contraseñas desde otro dispositivo** | 🔐 Cambia contraseñas de Gmail, redes sociales, banca, etc. Activa MFA (doble factor). |
| 6️⃣ | **Revocar sesiones activas** | ❌ Cerrar sesiones desconocidas en Gmail u otras cuentas. |
| 7️⃣ | **Escanear con antivirus / EDR** | 🧩 Ejecutar análisis completo.<br>Ej.: *Windows Defender Offline*, *Malwarebytes*, *CrowdStrike*. |
| 8️⃣ | **Revisar persistencia** | 🕵️‍♂️ Revisar **tareas programadas**, **clave Run**, **crontab** o **systemd**. |
| 9️⃣ | **Bloquear salida SMTP** | 🚫 En firewall, bloquear puertos `25`, `465`, `587` para hosts no autorizados. |
| 🔟 | **Notificar a Seguridad/TI** | 📢 Informar a equipo de seguridad, CSIRT o responsable TI. |

---

## ✅ Checklist de Contención Rápida

| Estado | Tarea | Comentario |
|:--:|:--|:--|
| ☐ | Desconectado de red | — |
| ☐ | Proceso malicioso finalizado | — |
| ☐ | Contraseñas cambiadas (MFA activado) | — |
| ☐ | Archivos maliciosos eliminados | — |
| ☐ | Escaneo antimalware completado | — |
| ☐ | Revisadas tareas programadas y `crontab` | — |
| ☐ | Salida SMTP bloqueada | — |
| ☐ | Equipo de seguridad notificado | — |

---

## 🧾 Notas de Evidencia

| Campo | Descripción |
|:--|:--|
| **Fecha/Hora detección** | `YYYY-MM-DD HH:MM` |
| **Host afectado** | Nombre o IP |
| **PID / proceso** | Ej. `python.exe (PID 1234)` |
| **Archivos hallados** | Rutas completas |
| **Acciones realizadas** | Lista cronológica con hora |
| **Responsable de contención** | Nombre y contacto |
| **Estado actual** | Aislado / Limpio / En análisis |

---



