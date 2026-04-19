# 🤖 Headhunter Virtual con IA | End-to-End Data & Automation Solution

> Transformando correos de LinkedIn en decisiones estratégicas de empleo mediante IA, automatización y Business Intelligence.

---

## Elevator Pitch

Diseñé una solución end-to-end de datos e IA para automatizar la priorización de oportunidades laborales. El flujo realiza ingesta automática desde Gmail, ETL de texto no estructurado, extracción semántica con LLM, cálculo de compatibilidad mediante algoritmo propio en JavaScript, generación dinámica de CV y visualización ejecutiva en Looker Studio.

---

## 📸 Vista del Proyecto

![Scores y Métricas Clave](01_Scores_y_métricas_clave.png)

![Flujo n8n Completo](02_Flujo_n8n.png)

![Dashboard Looker Studio](03_Dashboard_Looker_Studio.png)

---

## 🎯 El Problema de Negocio

La búsqueda de empleo es un proceso ineficiente de emparejamiento de datos (data matching). El objetivo de este proyecto no es solo capturar alertas de vacantes, sino optimizar el tiempo y priorizar las oportunidades con mayor probabilidad de ajuste a un perfil técnico maestro, transformando ruido (correos) en decisiones estratégicas.

---

## 🔄 El Ciclo Completo del Dato

```
Captura → Transformación (ETL) → IA (NLP) → Scoring → Decisión → Acción → Almacenamiento → Visualización
```

---

## 🛠️ Arquitectura Técnica y Fases del Proyecto

| Fase | Implementación Técnica en n8n | Valor de Negocio |
|------|-------------------------------|-----------------|
| 1. Ingesta de Datos (Extract) | `Gmail Trigger` + `Get Message` para capturar HTML y texto plano de alertas laborales | Automatización de entrada de datos en tiempo real |
| 2. Transformación (ETL) | Nodo `Preparar prompt` (JS): limpieza de HTML, normalización, eliminación de ruido y límite de 8,000 caracteres | Convertir texto no estructurado en datos procesables |
| 3. IA / NLP | Integración API Groq (Llama 3.3 70B) con salida JSON estructurada e inferencia semántica | Extracción automática de entidades, requisitos y roles |
| 4. Matching / Scoring | Algoritmo propio en JS con reglas semánticas y ponderación doble (Técnico / Estratégico) | Medición cuantitativa del ajuste perfil-vacante |
| 5. Priorización | Ranking por `Puntaje Total` y selección del Top 2 usando funciones de array (`slice(0,2)`) | Foco exclusivo en oportunidades de mayor probabilidad |
| 6. Generación de Documentos | Template dinámico para CV y Carta de Presentación HTML adaptada al puesto | Personalización masiva y rápida (CV listo en < 2 min) |
| 7. Automatización (Acción) | Nodo `Send a message` vía Gmail para entregar el paquete final listo para postular | Acción automática sobre los insights generados |
| 8. Persistencia (DB) | Google Sheets automatizado — guarda: Fecha, Empresa, Score, Modalidad y Coincidencias | Trazabilidad total y auditoría de la información |
| 9. Visualización (BI) | Dashboard en Looker Studio interactivo con KPIs de mercado, tendencias y análisis por empresa | Inteligencia de mercado laboral y toma de decisiones basada en datos |

---

## 🧠 Algoritmo de Scoring

El núcleo de la toma de decisiones es un modelo de evaluación cuantitativa:

```
Puntaje Total = 0.70 × (Score Técnico) + 0.30 × (Score Estratégico)
```

- **Score Técnico:** Cruce de requisitos duros de la vacante vs. perfil base con reglas de coincidencia exacta y semántica
- **Score Estratégico:** Evaluación del sector (foco en Banca/Finanzas) y tamaño de la empresa. La modalidad se registra para análisis visual pero no afecta el puntaje

---

## 📊 Inteligencia de Mercado — Resultados

El módulo de Business Intelligence (Looker Studio) extrae inteligencia del mercado laboral en tiempo real:

- **20 ofertas procesadas** de alertas reales de LinkedIn
- **5 empresas analizadas:** BAC, ASTAY, Joveo AI, BAC Shared Services, PepsiCo
- **Mejor Match alcanzado:** 76% — Científico de datos / Data Scientist (ASTAY / Joveo AI)
- **Tendencia de modalidad:** 50% de roles híbridos para posiciones de Data Science / Analytics
- **CV personalizado generado en menos de 2 minutos** por ejecución

🔗 **[Ver Dashboard en vivo — Looker Studio](https://datastudio.google.com/reporting/758c49db-a498-4e68-a247-48294c847401/page/mUcvF)**

---

## ⚙️ Stack Tecnológico

| Capa | Tecnología |
|------|-----------|
| Orquestación | n8n |
| LLM / Procesamiento | Groq API · Llama 3.3 70B |
| Lógica de Negocio | JavaScript (ES6) |
| Almacenamiento | Google Sheets |
| Visualización / BI | Looker Studio |
| Integraciones | Gmail API |

---

## 🚀 Instalación y Uso

### 1. Clonar el repositorio
```bash
git clone https://github.com/fsotoeu-cyber/headhunter-automatico-n8n.git
```

### 2. Importar el workflow en n8n
1. Abre tu instancia de n8n
2. Ve a **Workflows → Import from file**
3. Selecciona `workflow.json`

### 3. Configurar la API Key de Groq
En el nodo **HTTP Request**, reemplaza el header `Authorization`:
```
Bearer YOUR_GROQ_API_KEY
```
por tu key real de Groq (formato: `gsk_...`). Obtén una gratis en [console.groq.com](https://console.groq.com).

### 4. Conectar credenciales OAuth2
En los nodos de **Gmail** y **Google Sheets**, conecta tus cuentas desde n8n.

### 5. Activar el workflow
Clic en **Activate** — se ejecutará automáticamente con cada alerta de LinkedIn.

---

## 🔐 Variables de Referencia

```env
GROQ_API_KEY=your_groq_api_key_here        # Formato: gsk_...
GMAIL_RECIPIENT=your_email@gmail.com
GSHEETS_HISTORIAL_ID=your_google_sheet_id
GSHEETS_VACANTES_ID=your_google_sheet_id
```

---

## 🗺️ Roadmap

- [ ] Nodo de Telegram para notificación informal en tiempo real
- [ ] Scoring de idiomas y modalidad en el algoritmo
- [ ] Soporte para múltiples fuentes (Indeed, Computrabajo)
- [ ] Expansión del dashboard con análisis de tendencias semanales

---

## 👤 Autor

**Fausto Soto**
Industrial Engineer & Data Scientist
📍 Tegucigalpa, Honduras
🔗 [LinkedIn](https://www.linkedin.com/in/fausto-soto)
🤖 [ChurnInsight v3.0](https://poe.com/Churn_ROI_Architect) — ROI 8.10x | Recall 96.52%

---

## 📄 Licencia

MIT License — libre para usar, modificar y distribuir con atribución.

---

> *"Transformar criterios subjetivos en lógica ejecutable y resultados medibles."*
