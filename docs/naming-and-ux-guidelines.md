# Guía de Naming & UX para flujos n8n

Este documento define las convenciones de naming, estructura y mensajes UX para todos los workflows y nodos de n8n en este proyecto.

> **Cuándo y por qué usar cada convención**

Las **naming conventions** te ayudan a mantener coherencia y escalabilidad cuando el equipo crea nuevos workflows y nodos: identificas de un vistazo el dominio de negocio, la versión y el tipo de recurso.

Los **UX messages** con emojis y placeholders facilitan la monitorización y el troubleshooting en tiempo real; los desarrolladores y operadores saben inmediatamente si un paso falló, qué datos procesó o si todo salió OK.
> 

## **Naming conventions**

| **Nivel** | **Prefijo** | **Ejemplo** | **Estructura de carpetas** |
| --- | --- | --- | --- |
| **Workflow** | wf_ | wf_customer-onboarding | /workflows/customer/onboarding/ |
| **Grupo** | grp_ | grp_data-sync | /workflows/data/sync/ |
| **Nodo** | node_ | node_fetchUserData | Dentro del JSON del workflow |
| **Credencial** | cred_ | cred_mailchimp_api | /credentials/cred_mailchimp_api.json |

**Reglas clave**

- Usa **kebab-case** para filenames y **snake_case** para IDs internas.
- Carpeta raíz por dominio de negocio, subcarpeta por caso de uso.
- Versionado semántico opcional: añade _v1, _v2 antes de la extensión.

---

## **UX messages**

| **Tipo** | **Emoji** | **Ejemplo de mensaje** |
| --- | --- | --- |
| **Éxito** | ✅ | "Usuario {{ $json.email }} registrado con éxito." |
| **Error** | ❌ | "Error al enviar email: {{ $json.error.message }}." |
| **Notificación** | 🔔 | "Se han procesado {{ $json.count }} registros correctamente." |

**Detalles**

- Usa {{ }} para variables dinámicas.
- Coloca el emoji al inicio para reconocimiento instantáneo.
- Añade estos mensajes en los campos settings.successMessage y settings.errorMessage de los nodos críticos.

---
