flowchart LR
  A[Removable Media<br/>Initial Access<br/>T1091 / T1204]
  B[Keylogging<br/>Input Capture / Keylogging<br/>T1056.001<br/><small>pynput.keyboard</small>]
  C[Video Capture<br/>Video Capture<br/>T1125<br/><small>cv2.VideoCapture(0) → .mp4</small>]
  D[System & Network Discovery<br/>T1082 / T1016<br/><small>psutil, platform, socket</small>]
  E[Exfiltration via SMTP<br/>T1048 / T1071.003<br/><small>smtplib → smtp.gmail.com:587</small>]
  F[Artefactos / IoCs<br/><small>Data_Video, Data_Archivo_txt, .pickle, credenciales en claro</small>]

  A -->|usuario conecta y ejecuta| B
  B --> C
  B --> D
  C --> D
  D --> E
  E --> F

