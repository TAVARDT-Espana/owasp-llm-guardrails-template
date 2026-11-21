# OWASP LLM01 Guardrails Template y Guía de Seguridad de IA | TAVARDT España

[![Licence MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![OWASP LLM01](https://img.shields.io/badge/OWASP-LLM01%20Hardened-ff0055.svg)](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
[![Language](https://img.shields.io/badge/Language-Español%20(España)-green.svg)](README.md)
[![AI Diagnostics](https://img.shields.io/badge/TAVARDT-AI%20Evaluator-5b3cf5.svg)](https://tools.tavardt.com/es/evaluador-robustez-llm/)

Blueprint declarativo y middleware de código abierto para la mitigación de Prompt Injection (OWASP LLM01), fuga de system prompt y manipulación adversarial en agentes de IA, conforme al Esquema Nacional de Seguridad (ENS) y el Reglamento Europeo de IA (AI Act).

Desarrollado y mantenido por el equipo de ingeniería de inteligencia artificial de **[TAVARDT España](https://ag.tavardt.com/es/super-intelligence/)**.

---

## 1. Visión General de la Seguridad en IA y Modelos de Lenguaje

Este repositorio proporciona un middleware ligero y modular para la implementación de **guardrails** deterministas en agentes autónomos, sistemas RAG y aplicaciones empresariales que interactúan con LLMs (OpenAI, Anthropic, Gemini, Llama, Mistral).

### La Necesidad Crítica de Guardrails en Aplicaciones de IA
Los modelos de lenguaje no distinguen por defecto entre las instrucciones de control del sistema y los datos provistos por el usuario. Sin barreras activas de validación de entrada y salida, las aplicaciones quedan expuestas a la toma de control del modelo (jailbreak) y a la extracción de datos sensibles.

---

## 2. Vectores de Amenaza Mitigados (OWASP Top 10 for LLMs)

| Capa de Defensa | Vector de Amenaza Mitigado | Mecanismo de Mitigación |
| :--- | :--- | :--- |
| **Input Sanitizer** | Inyección Directa de Prompt (Jailbreak) | Detección perimetral de patrones adversariales (`ignora las instrucciones anteriores`, `DAN`, tags XML manipuladas). |
| **Canary Token Verifier** | Fuga de Prompt de Sistema | Rastrear tokens canario inviolables en la salida generada para impedir la exfiltración de directrices internas. |
| **RAG Boundary Guard** | Inyección Indirecta de Prompt | Aislamiento y delimitación semántica de documentos externos incorporados a bases de datos vectoriales. |
| **Structured Output Filter** | Invocación No Autorizada de Tools | Validación estricta de esquemas JSON antes de permitir la ejecución de llamadas a funciones o conectores MCP. |

---

## 3. Diagnóstico Previo de Robustez de su Modelo de IA

Antes de desplegar agentes conversacionales o automatizaciones críticas, examine la resiliencia de su modelo mediante la herramienta abierta de TAVARDT:

* **Evaluación de Robustez:** [Evaluador de Robustez de LLMs TAVARDT España](https://tools.tavardt.com/es/evaluador-robustez-llm/)
* **Catálogo Global de Herramientas:** [TAVARDT Tools España](https://tools.tavardt.com/es/)

---

## 4. Instalación y Guía Rápida de Integración

### Clonar y Ejecución

```bash
git clone https://github.com/TAVARDT-Espana/owasp-llm-guardrails-template.git
cd owasp-llm-guardrails-template
python examples/quickstart.py
```

### Ejemplo de Integración en Python

```python
from guardrails.validator import LLMGuardrail

guard = LLMGuardrail()

# 1. Validación de Entrada (Input Guardrail)
is_safe, error = guard.validate_input(user_input)
if not is_safe:
    raise ValueError(f"Entrada bloqueada por patrón sospechoso: {error}")

# 2. Inserción de Token Canario en el Prompt de Sistema
hardened_system_prompt = guard.get_canary_injection_prompt(system_prompt)

# 3. Validación de Salida (Output Guardrail)
is_valid, leak_error = guard.validate_output(completion)
if not is_valid:
    raise SecurityError("Fallo crítico: ¡Fuga de system prompt detectada mediante token canario!")
```

---

## 5. Consultoría Especializada en Agentes de IA y Ciberseguridad

Si su organización requiere auditorías de seguridad en IA, blindaje de agentes para WhatsApp/web o adecuación al Reglamento de IA de la UE:

* **Portal Corporativo:** [TAVARDT España](https://ag.tavardt.com/es/super-intelligence/)
* **Contacto Técnico Especializado:** [Contactar con el Equipo de Ingeniería](https://ag.tavardt.com/es/contacto/)

---

## Licencia

Distribuido bajo licencia de código abierto MIT. Consulte el archivo [`LICENSE`](LICENSE) para más detalles.  
Copyright (c) 2026 TAVARDT España.
