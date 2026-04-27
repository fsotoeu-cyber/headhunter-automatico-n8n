# 🤖 Headhunter Virtual con IA | End-to-End Data & Automation Solution

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> Transformando correos de LinkedIn en decisiones estratégicas de empleo mediante IA, automatización y Business Intelligence.  
> **+136 vacantes evaluadas · A/B Testing integrado · Radar de mercado en producción.**

---

## Elevator Pitch

Diseñé una solución end-to-end de datos e IA para automatizar la priorización de oportunidades laborales. El flujo realiza ingesta automática desde Gmail, ETL de texto no estructurado, extracción semántica con LLM, cálculo de compatibilidad mediante algoritmo propio en JavaScript, generación dinámica de CV y visualización ejecutiva en Looker Studio.

---

## 📸 Vista del Proyecto

![Scores](assets/screenshots/01_Scores%20_y%20_metricas%20_clave.png)

![Flujo](assets/screenshots/02_Flujo%20_n8n.png)

![Dashboard](assets/screenshots/03_Dashboard%20_Looker_Studio.png)

---

## 🎯 El Problema de Negocio

La búsqueda de empleo es un proceso ineficiente de emparejamiento de datos.  
Este sistema no solo captura alertas; optimiza el tiempo, prioriza las oportunidades con mayor probabilidad de ajuste y **transforma ruido en decisiones estratégicas**.

---

## 🔄 El Ciclo Completo del Dato

```
Captura → Transformación (ETL) → IA (NLP) → Scoring → Decisión → Acción → Almacenamiento → Visualización
```

---

## 🛠️ Arquitectura Técnica y Fases del Proyecto

| Fase | Implementación Técnica en n8n | Valor de Negocio |
|------|-------------------------------|-----------------|
| 1. Ingesta de Datos (Extract) | `Gmail Trigger` + `Get Message` para capturar HTML y texto plano de alertas laborales | Automatización de entrada de datos 24/7 |
| 2. Transformación (ETL) | Nodo `Preparar prompt` (JS): limpieza de HTML, normalización, eliminación de ruido y límite de 12,000 caracteres | Convertir texto no estructurado en datos procesables |
| 3. IA / NLP | Integración API Groq (Llama 3.3 70B) con salida JSON estructurada e inferencia ética de requisitos | Extracción automática de entidades, requisitos y roles |
| 4. Matching / Scoring | Algoritmo propio en JS con reglas semánticas y ponderación (70% Técnico / 30% Estratégico) | Medición cuantitativa del ajuste perfil-vacante |
| 5. Priorización | Ranking por `Puntaje Total` y selección del Top 2 usando funciones de array (`slice(0,2)`) | Foco exclusivo en oportunidades de mayor probabilidad |
| 6. Generación de Documentos | Template dinámico para CV y Carta de Presentación HTML adaptada al puesto | Personalización masiva y rápida (CV listo en < 2 min) |
| 7. Automatización (Acción) | Nodo `Send a message` vía Gmail para entregar el paquete final listo para postular | Acción automática sobre los insights generados |
| 8. Persistencia (DB) | Google Sheets automatizado — guarda puntajes, coincidencias, faltantes, modalidad, ubicación | Trazabilidad total y auditoría de la información |
| 9. Visualización (BI) | Dashboard en Looker Studio interactivo con KPIs de mercado, mapa geográfico y ranking de empresas | Inteligencia de mercado laboral y toma de decisiones basada en datos |

---

## 🧠 Algoritmo de Scoring

El núcleo de la toma de decisiones es un modelo de evaluación cuantitativa:

```
Puntaje Total = 0.70 × (Score Técnico) + 0.30 × (Score Estratégico)
```

- **Score Técnico:** Cruce de requisitos duros de la vacante vs. perfil base con reglas de coincidencia exacta, subcadena y semántica (más de 14 reglas específicas)
- **Score Estratégico:** Evaluación del sector (foco en Banca/Finanzas) y tamaño de la empresa

---

## 🧪 A/B Testing y Diagnóstico Automático

El flujo incorpora un **módulo de A/B Testing** que permite comparar la compatibilidad actual (**Score A**) contra la compatibilidad potencial si se cerraran todas las brechas de habilidades (**Score B**).  
La diferencia entre ambos scores cuantifica el valor de cada habilidad, y el sistema genera automáticamente un **ranking de gaps** para orientar el aprendizaje futuro.

📊 **Próxima evolución:** Integración de scoring cultural (tono organizacional, valores) sugerido por la comunidad.

---

## 📊 Inteligencia de Mercado — Resultados

El módulo de Business Intelligence (Looker Studio) extrae inteligencia del mercado laboral en tiempo real:

- **136 vacantes evaluadas** desde abril de 2026
- **50+ empresas analizadas**, incluyendo BAC, Banamex, PepsiCo, Softtek, Deloitte, Banco Davivienda, Grupo Ficohsa
- **Mejor Match alcanzado:** 79% — Portafolio Analytics Team Lead (BAC Shared Services) y otros roles en banca
- **Tasa de match perfecto (100% técnico):** 18 vacantes identificadas
- **Principio GIGO:** Los campos no disponibles aparecen como `null`; el sistema nunca inventa datos
- **Modalidades detectadas:** Remoto, Híbrido, Presencial — correctamente clasificadas
- **CV personalizado generado en menos de 2 minutos** por ejecución

🔗 **[Ver Dashboard en vivo — Looker Studio](https://datastudio.google.com/s/gVJ_qeQiekE)**

---

## ⚙️ Stack Tecnológico

| Capa | Tecnología |
|------|-----------|
| Orquestación | n8n (Cloud Starter) |
| LLM / Procesamiento | Groq API · Llama 3.3 70B |
| Lógica de Negocio | JavaScript (ES6) |
| Almacenamiento | Google Sheets (Historial, Rankings, A/B Test) |
| Visualización / BI | Looker Studio |
| Integraciones | Gmail API |

---

## 🚀 Instalación y Uso

### 1. Clonar el repositorio
```bash
git clone https://github.com/fsotoeu-cyber/headhunter-automatico-n8n.git

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
- [ ] Integración de análisis de tono organizacional y scoring cultural (con auditoría humana)
- [ ] Expansión del A/B Testing para comparar modelos de IA
- [ ] Soporte para ingesta de PDFs y fuentes externas (Indeed, Computrabajo)
- [ ] Dashboard avanzado con tendencias semanales y predicción de demanda de habilidades

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
