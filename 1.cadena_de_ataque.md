
---

## 🧠 Diagrama de cadena de ataque 


```mermaid
flowchart LR
  subgraph Initial_Access [Acceso inicial]
    direction TB
    A[/"Medio extraíble\nT1091 / T1204"/]
  end

  subgraph Collection [Execution]
    direction TB
    B[/"Keylogging\nT1056.001\n(entrada)"/]
    C[/"Captura de vídeo\nT1125\n(dispositivo de cámara)"/]
  end

  subgraph Discovery [Descubrimiento]
    direction TB
    D[/"System & Network\nT1082 / T1016\n(info de sistema y red)"/]
  end

  subgraph Exfiltration [Exfiltracion]
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
  classDef box fill:#ffffff,stroke:#333,stroke-width:1px,font-size:24px,color:#000000,padding:10px;
  class A,B,C,D,E,F box;

  %% Estilo títulos subgráficos
  style Initial_Access font-size:18px;
  style Collection font-size:18px;
  style Discovery font-size:18px;
  style Exfiltration font-size:18px;
  style Artifacts font-size:18px;

  %% Fondos por táctica
  style Initial_Access fill:#000000,stroke:#e67e22,stroke-width:1px;
  style Collection fill:#000000,stroke:#1f78b4,stroke-width:1px;
  style Discovery fill:#000000,stroke:#2e8b57,stroke-width:1px;
  style Exfiltration fill:#000000,stroke:#c0392b,stroke-width:1px;
  style Artifacts fill:#000000,stroke:#95a5a6,stroke-width:1px;

  linkStyle default stroke:#444,stroke-width:2px;
