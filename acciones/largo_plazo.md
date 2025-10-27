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

