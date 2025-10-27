# 🧠 Diagrama de Cadena de Ataque (versión simplificada)

Este diagrama muestra la secuencia de un ataque mediante un script malicioso, usando términos simples para usuarios no técnicos. Los códigos MITRE ATT&CK se mantienen para referencia técnica.

```mermaid
flowchart LR
  subgraph Acceso_Inicial [Acceso Inicial]
    direction TB
    A["USB o dispositivo externo\nT1091 / T1204"]
  end

  subgraph Recoleccion [Recolección de Información]
    direction TB
    B["Registro de teclas (Keylogger)\nT1056.001"]
    C["Grabación de vídeo con la cámara\nT1125"]
  end

  subgraph Descubrimiento [Descubrimiento del Sistema]
    direction TB
    D["Obtiene información del equipo y red\nT1082 / T1016"]
  end

  subgraph Exfiltracion [Envío de Información]
    direction TB
    E["Envía datos por correo electrónico\nT1048 / T1071.003"]
  end

  subgraph Evidencias [Archivos generados / IoCs]
    direction TB
    F["Archivos de video, texto y datos del usuario"]
  end

  %% Flujo
  A --> B
  B --> C
  B --> D
  C --> D
  D --> E
  E --> F

  %% Estilo de nodos (texto más grande y oscuro)
  classDef box fill:#ffffff,stroke:#333,stroke-width:1px,font-size:20px,color:#000000,padding:10px;
  class A,B,C,D,E,F box;

  %% Estilo títulos subgráficos
  style Acceso_Inicial font-size:16px;
  style Recoleccion font-size:16px;
  style Descubrimiento font-size:16px;
  style Exfiltracion font-size:16px;
  style Evidencias font-size:16px;

  %% Fondos por táctica
  style Acceso_Inicial fill:#f39c12,stroke:#e67e22,stroke-width:1px;
  style Recoleccion fill:#3498db,stroke:#1f78b4,stroke-width:1px;
  style Descubrimiento fill:#2ecc71,stroke:#27ae60,stroke-width:1px;
  style Exfiltracion fill:#e74c3c,stroke:#c0392b,stroke-width:1px;
  style Evidencias fill:#95a5a6,stroke:#7f8c8d,stroke-width:1px;

  linkStyle default stroke:#444,stroke-width:2px;
