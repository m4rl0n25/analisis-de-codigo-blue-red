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

## 🎯 Secuencia de tácticas y técnicas (MITRE ATT&CK)

| # | Táctica | Técnica (ID) | Descripción | Evidencia / Función en el script |
|---|----------|---------------|-------------|----------------------------------|
| 1 | **Initial Access** | [T1091 – Removable Media](https://attack.mitre.org/techniques/T1091/) / [T1204 – User Execution](https://attack.mitre.org/techniques/T1204/) | El código llega por USB y se ejecuta manualmente por el usuario. | Ejecución de `script.py` desde unidad extraíble. |
| 2 | **Collection / Execution** | [T1056.001 – Input Capture: Keylogging](https://attack.mitre.org/techniques/T1056/001/) | Registro de pulsaciones del teclado con `pynput.keyboard`. | Genera archivos `.pickle` o `.txt` con las teclas capturadas. |
| 3 | **Collection** | [T1125 – Video Capture](https://attack.mitre.org/techniques/T1125/) | Captura de video desde la cámara del sistema. | `cv2.VideoCapture(0)` → crea `.mp4` en `Data_Video/`. |
| 4 | **Discovery** | [T1082 – System Info Discovery](https://attack.mitre.org/techniques/T1082/) / [T1016 – Network Configuration Discovery](https://attack.mitre.org/techniques/T1016/) | Recolección de datos del sistema y red (hostname, IP, CPU, RAM). | Uso de `psutil`, `platform`, `socket`. |
| 5 | **Exfiltration** | [T1048 – Exfiltration Over Alternative Protocol](https://attack.mitre.org/techniques/T1048/) / [T1071.003 – Application Layer Protocol: Mail (SMTP)](https://attack.mitre.org/techniques/T1071/003/) | Envía los datos recolectados por correo. | `smtplib` → `smtp.gmail.com:587` con credenciales incrustadas. |

---

## 🧠 Diagrama de cadena de ataque

<details>
<summary>📊 Mostrar diagrama</summary>

```mermaid
flowchart LR
  subgraph Initial_Access [Initial Access]
    direction TB
    A[/"Medio extraíble\nT1091 / T1204"/]
  end

  subgraph Collection [Collection / Execution]
    direction TB
    B[/"Keylogging\nT1056.001\n(pynput)"/]
    C[/"Captura de vídeo\nT1125\n(cv2 → .mp4)"/]
  end

  subgraph Discovery [Discovery]
    direction TB
    D[/"System & Network\nT1082 / T1016\n(psutil, platform, socket)"/]
  end

  subgraph Exfiltration [Exfiltration]
    direction TB
    E[/"SMTP / Mail\nT1048 / T1071.003\n(smtplib)"/]
  end

  subgraph Artifacts [Artefactos / IoCs]
    direction TB
    F[/"Data_Video, .txt, .pickle,\ncredenciales en claro"/]
  end

  %% Flujo y estilos
  A --> B
  B --> C
  B --> D
  C --> D
  D --> E
  E --> F

  classDef box fill:#ffffff,stroke:#333,stroke-width:1px,font-size:18px,padding:10px;
  class A,B,C,D,E,F box;

  style Initial_Access fill:#fdebd0,stroke:#e67e22,stroke-width:1px;
  style Collection fill:#e8f6ff,stroke:#1f78b4,stroke-width:1px;
  style Discovery fill:#f0f5e6,stroke:#2e8b57,stroke-width:1px;
  style Exfiltration fill:#fff0f0,stroke:#c0392b,stroke-width:1px;
  style Artifacts fill:#f7f7f7,stroke:#95a5a6,stroke-width:1px;

  linkStyle default stroke:#444,stroke-width:2px;
