# 🧩 Análisis de cadena de ataque — Basado en MITRE ATT&CK

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Analysis-orange.svg)]

> **Resumen:** Análisis técnico y mapeo MITRE ATT&CK de una cadena de ataque que implica la llegada de un script malicioso vía medio extraíble. Este repositorio contiene únicamente documentación, diagramas y recomendaciones defensivas — **no** contiene código malicioso ni instrucciones de explotación.

---

## 📘 Resumen ejecutivo
El análisis modela una cadena de ataque típica donde un artefacto malicioso transportado por **memoria USB** es ejecutado por el usuario y realiza recolección de información y exfiltración. El objetivo de este repositorio es **documentar técnicas, Artefactos/IoC y medidas de mitigación** para uso educativo y defensivo.

### Acciones observadas (alto nivel)
- Captura de entradas (keylogging)
- Captura de vídeo desde cámara
- Recolección de información del sistema y red
- Exfiltración mediante correo (SMTP)

> ⚠️ **Nota importante:** Este proyecto es de propósito defensivo y de investigación. No se distribuye ni se documentan instrucciones para implementar código malicioso.

---

## 🎯 Mapeo a MITRE ATT&CK (resumen)
| # | Táctica | Técnica (ID) |
|---|---------|--------------|
| 1 | Initial Access | T1091 (Removable Media), T1204 (User Execution) |
| 2 | Collection / Execution | T1056.001 (Input Capture — Keylogging) |
| 3 | Collection | T1125 (Video Capture) |
| 4 | Discovery | T1082 (System Info Discovery), T1016 (Network Configuration Discovery) |
| 5 | Exfiltration | T1048 (Exfiltration Over Alternative Protocol), T1071.003 (Application Layer Protocol: Mail) |

---

## 🧠 Diagrama de cadena de ataque (Mermaid)
> GitHub soporta Mermaid en bloques de código. Pega el bloque tal cual en tu README para renderizado.

```mermaid
flowchart LR
  subgraph Initial_Access [Initial Access]
    direction TB
    A[/"Medio extraíble\nT1091 / T1204"/]
  end

  subgraph Collection [Collection / Execution]
    direction TB
    B[/"Keylogging\nT1056.001\n(entrada)"/]
    C[/"Captura de vídeo\nT1125\n(dispositivo de cámara)"/]
  end

  subgraph Discovery [Discovery]
    direction TB
    D[/"System & Network\nT1082 / T1016\n(info de sistema y red)"/]
  end

  subgraph Exfiltration [Exfiltration]
    direction TB
    E[/"SMTP / Mail\nT1048 / T1071.003\n(exfiltración)"/]
  end

  subgraph Artifacts [Artefactos / IoCs]
    direction TB
    F[/"Data_Video, *.txt, *.pickle,\ncredenciales en claro (ejemplo)"/]
  end

  %% Flujo
  A --> B
  B --> C
  B --> D
  C --> D
  D --> E
  E --> F

  %% Estilo de nodos (texto más grande y oscuro)
  classDef box fill:#ffffff,stroke:#333,stroke-width:1px,font-size:24px,color:#111111,padding:10px;
  class A,B,C,D,E,F box;

  %% Estilo títulos subgráficos
  style Initial_Access font-size:22px;
  style Collection font-size:22px;
  style Discovery font-size:22px;
  style Exfiltration font-size:22px;
  style Artifacts font-size:22px;

  %% Fondos por táctica
  style Initial_Access fill:#fdebd0,stroke:#e67e22,stroke-width:1px;
  style Collection fill:#e8f6ff,stroke:#1f78b4,stroke-width:1px;
  style Discovery fill:#f0f5e6,stroke:#2e8b57,stroke-width:1px;
  style Exfiltration fill:#fff0f0,stroke:#c0392b,stroke-width:1px;
  style Artifacts fill:#f7f7f7,stroke:#95a5a6,stroke-width:1px;

  linkStyle default stroke:#444,stroke-width:2px;

