# GuIA H.U. Dr. Peset

Asistente farmacoterapéutico web orientado a profesionales sanitarios del H.U. Dr. Peset.

## Qué incluye esta versión

- Chat clínico con enfoque en farmacoterapia, compatibilidad IV y estabilidad.
- Búsqueda rápida en fuentes oficiales (CIMA, FDA, EMA, PubMed, ClinicalTrials).
- Carga de documentación local del hospital (GFT, actas, protocolos, etc.).
- Panel de **Noticias** en la barra lateral.
- Pantalla secundaria de **Estadísticas y configuración**.
- Soporte de dos proveedores LLM:
  - **Llama Local (recomendado)**: sin API key.
  - **Claude Sonnet 4**: opcional con API key de Anthropic.

## Ejecución local

Este proyecto es una web estática (`index.html`).

```bash
python -m http.server 4173 --directory /workspace/GuIA
```

Luego abre:

- `http://127.0.0.1:4173/index.html`

## Uso sin API (Llama local)

La app arranca por defecto en modo **Llama Local**. Para que funcione, necesitas un servidor local compatible con Ollama en `127.0.0.1:11434`.

Pasos típicos:

```bash
ollama serve
ollama run llama3.1:8b
```

Cuando Ollama esté activo, GuIA enviará las consultas a `POST /api/chat` sin necesidad de API key.

## Uso con API (Claude)

Si prefieres Claude:

1. Haz clic en el badge **Claude Sonnet 4**.
2. Introduce una API key válida (`sk-ant-...`).
3. La clave se guarda en `localStorage` del navegador para reutilizarse.

## Notas

- Si Llama local no está disponible, la app mostrará un aviso con los pasos para iniciarlo.
- Si no hay API key y eliges Claude, la app abrirá el modal de configuración.


## Solución de problemas de conexión (Llama)

Si aparece "Llama local no disponible":

1. Abre **Estadísticas → Configuración** y revisa el campo **Endpoint Llama / Ollama**.
2. Prueba primero con `http://127.0.0.1:11434/api/chat` (local).
3. Si tu GuIA se sirve en HTTPS, usa un proxy HTTPS (por ejemplo `/api/ollama/chat`) para evitar bloqueo por *mixed content*.
4. Verifica Ollama:

```bash
ollama serve
ollama run llama3.1:8b
```
