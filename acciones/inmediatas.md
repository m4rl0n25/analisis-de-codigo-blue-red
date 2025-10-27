# 🧠 Guía de Respuesta por Incidente

Este cuadro resume las **acciones inmediatas** y las **acciones recomendadas a largo plazo** ante la ejecución de un script malicioso tipo *keylogger + grabador de webcam + exfiltrador SMTP*.

---

## ⚠️ Acciones Inmediatas (Contención y Remediación)

| **#** | **Acción** | **Descripción / Comando sugerido** |
|:--:|:--|:--|
| 1️⃣ | **Desconectar red** | 🔌 Desactiva Wi-Fi o desconecta cable Ethernet.<br>**Windows:** `netsh interface set interface "Wi-Fi" admin=disabled`<br>**Linux:** `nmcli networking off` |
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

## 🛡️ Acciones a Largo Plazo (Prevención y Resiliencia)

| **Categoría** | **Recomendación** | **Objetivo / Detalle** |
|:--|:--|:--|
| **1. Política IR** | Crear y mantener un *Plan de Respuesta a Incidentes (IR)*. | Define fases: detección → contención → erradicación → recuperación. |
| **2. Endpoint Protection (EDR)** | Implementar EDR/AV corporativo. | Detección de keyloggers, webcam access, conexiones SMTP sospechosas. |
| **3. Segmentación de red** | Restringir salidas SMTP/FTP. | Solo permitir conexiones necesarias. |
| **4. Gestión de secretos** | Eliminar credenciales en texto plano. | Usar *Vaults* o *Secret Managers* (HashiCorp Vault, AWS SM). |
| **5. Menor privilegio** | Ejecutar scripts con mínimos permisos. | Evitar ejecución con `sudo` o `admin` innecesario. |
| **6. Control de periféricos** | Restringir acceso a cámara y micrófono. | Políticas GPO o configuración de permisos. |
| **7. Secure Coding** | Revisar código y evitar `pickle`. | Usar `json` o formatos seguros, revisión de pares. |
| **8. Monitoreo / DLP** | Implementar DLP + SIEM. | Detectar exfiltración y registrar actividad. |
| **9. Backups y recuperación** | Hacer copias offline verificadas. | Evita pérdida de datos tras infección. |
| **10. Capacitación** | Formar a usuarios. | Evita ejecución de scripts desconocidos. |
| **11. Auditorías y pruebas** | Pentesting y phishing tests periódicos. | Detectar debilidades antes de que se exploten. |

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

## 📁 Estructura sugerida del repositorio

| Carpeta / Archivo | Contenido |
|:--|:--|
| `README.md` | Este resumen y guía general. |
| `docs/playbook.md` | Guía extendida paso a paso. |
| `scripts/neutralized/` | Scripts sin código malicioso (para estudio). |
| `infra/firewall_rules.md` | Configuración de bloqueo y segmentación. |
| `.github/workflows/ci.yml` | CI para lint/test. |
| `.gitignore` | Evita subir secretos o datos. |

---

## 🧰 Comandos Git básicos

| Acción | Comando |
|:--|:--|
| Clonar repo | `git clone https://github.com/tu-usuario/ir-playbook.git` |
| Crear rama | `git checkout -b feature/add-playbook` |
| Añadir cambios | `git add .` |
| Commit | `git commit -m "Añadir guía IR inicial"` |
| Push | `git push -u origin feature/add-playbook` |
| Crear PR | Desde GitHub → *Pull Request → main* |

---

> 📌 **Nota:** Este cuadro puede copiarse tal cual en un archivo `README.md` o `docs/IR-summary.md` dentro de tu repositorio GitHub.  
> ¿Deseas que lo extienda con un bloque de código automatizable (por ejemplo, comandos en Bash/PowerShell para aplicar todo el checklist)? Puedo generarlo también.

