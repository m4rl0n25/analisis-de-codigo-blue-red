# 🧩 Análisis de cadena de ataque — Basado en MITRE ATT&CK

## 📘 Resumen ejecutivo
Este análisis describe una cadena de ataque donde un **script malicioso** llega al sistema a través de una **memoria USB**.  
Al ser ejecutado, realiza las siguientes acciones:

- Captura de teclas (keylogger con `pynput`)
- Grabación de video con la cámara (`cv2.VideoCapture`)
- Recolección de información del sistema y red (`psutil`, `platform`, `socket`)
- Exfiltración de los datos por correo (`smtplib` → `smtp.gmail.com:587`)

El siguiente mapeo usa el **framework MITRE ATT&CK** para identificar tácticas y técnicas empleadas.

---

## 1️⃣ Matriz MITRE DEFEND (Contramedidas)

| Táctica / Técnica DEFEND | Descripción | Medida recomendada |
|---------------------------|------------|------------------|
| **Endpoint Detection** | Detección de actividad sospechosa en endpoints. Para referencia MITRE: [ED0010 – Endpoint Security Software](https://attack.mitre.org/mitigations/ED0010/) | Uso de antivirus/EDR que monitorice keyloggers, accesos a cámara y manipulación de ficheros sensibles |
| **Network Protection** | Control de tráfico saliente. MITRE: [NT0040 – Network Intrusion Prevention](https://attack.mitre.org/mitigations/NT0040/) | Bloquear conexiones SMTP no autorizadas, inspección de tráfico TLS/SSL |
| **Account Protection** | Protección de credenciales y contraseñas. MITRE: [AC0001 – Account Use Policies](https://attack.mitre.org/mitigations/AC0001/) | Uso de gestores de contraseñas, MFA, no almacenar credenciales en texto plano |
| **Audit / Logging** | Registro de actividad de usuario y procesos. MITRE: [AU0001 – Audit](https://attack.mitre.org/mitigations/AU0001/) | Auditoría de procesos Python sospechosos, registros de creación de carpetas y archivos en ubicaciones críticas |
| **Application Hardening** | Prevención de ejecución de scripts maliciosos. MITRE: [AP0001 – Application Isolation & Sandboxing](https://attack.mitre.org/mitigations/AP0001/) | Políticas de ejecución restringida, sandboxing, whitelisting de aplicaciones confiables |
| **User Training / Awareness** | Educación del usuario sobre riesgos. MITRE: [UA0001 – Security Awareness Training](https://attack.mitre.org/mitigations/UA0001/) | Capacitación sobre phishing, dispositivos externos y ejecución de scripts desconocidos |
| **Data Protection** | Protección de información sensible. MITRE: [DP0001 – Data Loss Prevention](https://attack.mitre.org/mitigations/DP0001/) | Cifrado de archivos, control de acceso a datos críticos y monitorización de exfiltración |
