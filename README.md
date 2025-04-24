
# 📁 Honeypot Logs - Infraestructura Local

## 🧭 Introducción

Este proyecto contiene la estructura y comandos necesarios para ejecutar y gestionar honeypots desde Docker en un entorno Windows. Todos los honeypots almacenan sus logs localmente dentro de la carpeta `C:/honeypot-logs`, por lo que es importante mantener esta ubicación para que los volúmenes funcionen correctamente.

---

## 🚀 Ejecución de Honeypots

Dirígete al archivo [`commands`](./commands) para encontrar los comandos necesarios para levantar cada honeypot. En general, cada honeypot tiene dos pasos:

1. `docker pull` → descarga la imagen del contenedor.
2. `docker run` → ejecuta el contenedor con los puertos y volúmenes correctamente mapeados.

---

## 🐍 Honeypots Configurados

### 🔷 Dionaea

- Especializado en capturar malware y detectar conexiones de puertos comunes de servicios vulnerables.
- Guarda logs en `C:/honeypot-logs/dionaea/dionaea.log` y `dionaea-errors.log`.
- Servicios habilitados configurables en `services-enabled/smb.yml`.

### 🔶 OpenCanary

- Honeypot modular que simula múltiples servicios como HTTP, FTP, SSH, etc.
- Configuración en `C:/honeypot-logs/opencanary/opencanary.conf`.
- Logs almacenados en `C:/honeypot-logs/opencanary/opencanary.log`.

### 🟡 Cowrie

- Simula un entorno SSH/Telnet falso para capturar interacciones con atacantes.
- Expone el puerto 2222 (en lugar del 22).
- Logs disponibles en `C:/honeypot-logs/crowie/cowrie.log`.

---

## 📄 Estructura del Repositorio

```
HONEYPOT-LOGS/
│
├── crowie/
│   └── cowrie.log        # Logs generados por Cowrie
│
├── dionaea/
│   ├── dionaea/
│   │   ├── dionaea.log          # Log principal
│   │   ├── dionaea-errors.log   # Errores
│   │   └── services-enabled/
│   │       └── smb.yml          # Servicios personalizados habilitados
│
├── opencanary/
│   ├── opencanary.conf    # Configuración principal
│   └── opencanary.log     # Log generado por OpenCanary
│
├── commands               # Comandos Docker de cada honeypot
└── README.md              # Este archivo
```

---

## 📊 Logs

Todos los honeypots están configurados para registrar su actividad en archivos `.log` dentro de `C:/honeypot-logs`. Puedes visualizarlos directamente con un editor como VSCode, Notepad++, etc. Para pruebas puedes usar herramientas como:

- [Nmap](https://nmap.org) para escaneo de puertos.
- Navegador web para interactuar con servicios HTTP/HTTPS (OpenCanary).
- Cliente FTP para simular conexiones al puerto 21.
- Cliente SSH apuntando a `localhost:2222` (Cowrie).

---

## ✅ Recomendaciones

- Asegúrate de tener los puertos libres antes de ejecutar los contenedores.
- Ejecuta Docker Desktop con privilegios de administrador.
- Si algún contenedor falla, revisa con `docker logs <nombre>` o elimina y vuelve a crear el contenedor.

---

## 🧪 Testing rápido

Ejemplo de escaneo local para generar tráfico:

```powershell
nmap -sS -sV -Pn -p 21,80,135,443,2222 localhost
```