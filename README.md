# Cadena de ataque (USB → exfiltración) — Diagrama interactivo

> Diagrama mermaid que muestra la secuencia de tácticas y técnicas (MITRE ATT&CK).
> Si no se renderiza en tu GitHub, prueba en https://mermaid.live/ o habilita Mermaid en tu visor de Markdown.

```mermaid
flowchart LR
  %% Nodes
  A[/"Removable Media\nInitial Access\nT1091 / T1204"/]
  B[/"Keylogging\nInput Capture / Keylogging\nT1056.001\n(pynput.keyboard)"/]
  C[/"Video Capture\nVideo Capture\nT1125\n(cv2.VideoCapture -> .mp4)"/]
  D[/"System & Network Discovery\nT1082 / T1016\n(psutil, platform, socket)"/]
  E[/"Exfiltration via SMTP\nT1048 / T1071.003\n(smtplib -> smtp.gmail.com:587)"/]
  F[/"Artefactos / IoCs\nData_Video, Data_Archivo_txt, .pickle, credenciales en claro"/]

  %% Edges / Flow
  A -->|Usuario conecta y ejecuta| B
  B --> C
  B --> D
  C --> D
  D --> E
  E --> F

  %% Styling por táctica (colores)
  classDef access fill:#fdebd0,stroke:#e67e22,stroke-width:1px;
  classDef collection fill:#e8f6ff,stroke:#1f78b4,stroke-width:1px;
  classDef discovery fill:#f0f5e6,stroke:#2e8b57,stroke-width:1px;
  classDef exfil fill:#fff0f0,stroke:#c0392b,stroke-width:1px;
  classDef artifacts fill:#f7f7f7,stroke:#95a5a6,stroke-width:1px,font-style:italic;

  class A access;
  class B collection;
  class C collection;
  class D discovery;
  class E exfil;
  class F artifacts;

  %% Optional: force left-to-right neatness
  linkStyle default stroke:#777,stroke-width:1px;

