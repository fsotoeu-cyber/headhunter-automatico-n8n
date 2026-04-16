# 🤖 AI Headhunter Automático — n8n + Google Drive + Gmail + Gemini

> Workflow de automatización que captura alertas de empleo, analiza la oferta con IA, compara con tu perfil profesional y genera un CV personalizado — todo sin intervención manual.

---

## 📋 ¿Qué hace este proyecto?

Cuando LinkedIn (u otra fuente) envía una alerta de empleo a tu correo, este flujo de n8n:

1. **Detecta el correo** automáticamente vía Gmail Trigger
2. **Extrae el texto** de la oferta laboral con IA (Gemini API)
3. **Descarga tu CV base** desde Google Drive y lo lee en formato PDF
4. **Fusiona** ambas fuentes (oferta + perfil) y **calcula compatibilidad**
5. **Genera un CV personalizado** adaptado a los requisitos de esa oferta
6. **Te lo envía por correo** listo para aplicar

---

## 🏗️ Arquitectura del flujo

```
Gmail Trigger
    │
    ▼
Get a Message
    │
    ▼
Extraer Texto (Code Node - Gemini API)
    │
    ▼
HTTP Request ──────────────────────────────────┐
(POST Gemini API)                              │
    │                                          │
    ▼                                          ▼
Code in JavaScript              Download File (Google Drive)
(Procesa respuesta IA)               │
    │                           Extract from PDF
    └──────────────┬────────────────────────────┘
                   ▼
                Merge
                  │
                  ▼
        Calcular Compatibilidad
                  │
                  ▼
             Generar CV
                  │
                  ▼
        Send a Message (Gmail)
```

---

## 🧰 Stack Tecnológico

| Herramienta | Uso |
|---|---|
| **n8n** | Orquestador del flujo de automatización |
| **Gmail API** | Trigger de entrada y envío de resultado |
| **Google Drive** | Almacenamiento del CV base en PDF |
| **Gemini API** | Extracción de información + análisis con IA |
| **JavaScript** | Procesamiento y transformación de datos |

---

## ⚙️ Requisitos previos

- Cuenta en [n8n.io](https://n8n.io) (cloud o self-hosted)
- Credenciales de Gmail configuradas en n8n (OAuth2)
- Credenciales de Google Drive configuradas en n8n (OAuth2)
- API Key de Google Gemini ([obtener aquí](https://aistudio.google.com/app/apikey))
- Tu CV en formato PDF almacenado en Google Drive

---

## 🚀 Instalación y uso

### 1. Clonar el repositorio
```bash
git clone https://github.com/fsotoeu-cyber/headhunter-automatico-n8n.git
cd headhunter-automatico-n8n
```

### 2. Importar el workflow en n8n
1. Abre tu instancia de n8n
2. Ve a **Workflows → Import from file**
3. Selecciona el archivo `workflow.json`

### 3. Configurar credenciales
En cada nodo que lo requiera, conecta tus credenciales:
- **Gmail Trigger** → credencial OAuth2 de Gmail
- **Get a Message** → misma credencial de Gmail
- **HTTP Request** → API Key de Gemini en el header `x-goog-api-key`
- **Download File** → credencial OAuth2 de Google Drive
- **Send a Message** → credencial Gmail de destino

### 4. Configurar variables
En el nodo **Download File**, actualiza el `File ID` con el ID de tu CV en Google Drive.

> El ID está en la URL de tu archivo: `drive.google.com/file/d/**ESTE_ES_EL_ID**/view`

### 5. Activar el workflow
Haz clic en **Activate** en la esquina superior derecha de n8n.

---

## 📁 Estructura del repositorio

```
headhunter-automatico-n8n/
├── workflow.json          # Flujo exportado de n8n (importar directamente)
├── README.md              # Este archivo
├── screenshot.png         # Vista del workflow en n8n
└── .env.example           # Variables de entorno de referencia
```

---

## 🔐 Variables de entorno

Copia `.env.example` a `.env` y completa tus valores:

```env
GEMINI_API_KEY=tu_api_key_aqui
GDRIVE_FILE_ID=id_de_tu_cv_en_google_drive
GMAIL_RECIPIENT=tu_correo@gmail.com
```

> ⚠️ Nunca subas tu `.env` real al repositorio. Ya está en el `.gitignore`.

---

## 💡 Casos de uso

- Automatizar aplicaciones a empleos mientras duermes
- Personalizar tu CV para cada oferta sin esfuerzo manual
- Filtrar oportunidades según tu perfil antes de invertir tiempo
- Escalar tu búsqueda de empleo con IA

---

## 🗺️ Roadmap

- [ ] Soporte para múltiples fuentes de alertas (Indeed, Computrabajo)
- [ ] Scoring de compatibilidad con escala numérica
- [ ] Almacenamiento de historial de aplicaciones en Google Sheets
- [ ] Notificación por WhatsApp vía Twilio
- [ ] Dashboard de seguimiento en Notion

---

## 👤 Autor

**Fausto Soto**  
Industrial Engineer & Data Scientist  
📍 Tegucigalpa, Honduras  
🔗 [LinkedIn](https://www.linkedin.com/in/tu-perfil)  
🏗️ [ChurnInsight v3.0](https://poe.com/Churn_ROI_Architect) — ROI 8.10x | AUC-ROC 0.8381

---

## 📄 Licencia

MIT License — libre para usar, modificar y distribuir con atribución.

---

> *"La búsqueda de empleo también puede automatizarse con IA."*
