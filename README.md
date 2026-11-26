# Business Audit AI

Herramienta que genera una **auditoría digital completa de un negocio con IA** en unos 30 segundos. El usuario carga su web, su Instagram y su rubro, y recibe un informe profesional en pantalla y por email.

🔗 **Demo en vivo:** https://auton8n.netlify.app/

## Cómo funciona

```
Formulario web ──► Webhook n8n ──► Descarga del sitio
                                ──► Google PageSpeed (mobile)
                                ──► Prompt + datos ──► Groq (Llama 3.3 70B)
                                ──► Informe HTML ──► Respuesta al navegador
                                                 ──► Email al usuario
                                                 ──► Registro en Google Sheets
```

1. **Formulario (`index.html`):** pide sitio web, email, usuario de Instagram y rubro (e-commerce, gastronomía, salud, turismo, etc.). Mientras procesa, muestra los pasos: analizando sitio, métricas SEO, IA y generación del reporte.
2. **Workflow de n8n (`business-audit-ai.workflow.json`):**
   - Recibe los datos por webhook.
   - Descarga el HTML del sitio y extrae el texto.
   - Consulta **Google PageSpeed Insights** y obtiene Performance, SEO, Accesibilidad, FCP, LCP y CLS.
   - Arma un prompt con todo y lo manda a **Groq** (`llama-3.3-70b-versatile`), que devuelve un JSON estructurado.
   - Convierte ese JSON en un informe HTML con botón para descargar en PDF.
   - Lo devuelve al navegador, lo manda por email y guarda el lead en Google Sheets.

## Qué incluye el informe

- **Puntaje general** y resumen ejecutivo.
- **Marketing:** presencia digital, branding, redes sociales, fortalezas y mejoras.
- **SEO:** análisis técnico, velocidad, contenido, problemas y acciones concretas.
- **Competencia:** panorama, posicionamiento, ventajas, desventajas y diferenciación.
- **Plan de crecimiento:** oportunidades, quick wins, plan a 30, 60 y 90 días y KPIs para medir.

## Puesta en marcha

1. Importá `business-audit-ai.workflow.json` en n8n.
2. En el nodo **Groq API**, reemplazá `PEGAR_AQUI_TU_GROQ_API_KEY` por tu API key de Groq.
3. Configurá las credenciales SMTP en **Send Email** y poné tu email de remitente.
4. (Opcional) Cambiá la URL del nodo **Save to Google Sheets** por tu propio Apps Script.
5. Activá el workflow y, en `index.html`, poné la URL de producción de tu webhook.

## Tecnología

- Front: HTML, CSS y JavaScript vanilla.
- Automatización: n8n.
- IA: Groq API (Llama 3.3 70B).
- Datos: Google PageSpeed Insights API.

---

Proyecto de **Sebastián Soba**.
