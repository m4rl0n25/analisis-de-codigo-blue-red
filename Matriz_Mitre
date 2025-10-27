flowchart LR
  A[Removable Media\nInitial Access\nT1091 / T1204]
  B[Keylogging\nInput Capture\nT1056.001\n(pynput)]
  C[Video Capture\nT1125\n(cv2)]
  D[System & Network Discovery\nT1082 / T1016\n(psutil, socket)]
  E[Exfiltration via SMTP\nT1048 / T1071.003\n(smtplib)]
  A --> B
  B --> C
  B --> D
  C --> D
  D --> E
