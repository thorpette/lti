# Specification

Version 1 | 2026-05-18T17:15:34.943548+00:00 | Generado por IA (deepseek-pro) — 10 requirements

By: oscar.hidalgo.puertas@gmail.com

**Title:** Requirements iniciales (IA)
**Mode:** requirements_only

## Requirements (10)

### 1. Registro de candidato
El candidato puede crear una cuenta con email y contraseña, verificando el formato del email y la fortaleza de la contraseña. Tras el registro exitoso recibe confirmación y acceso al sistema.

### 2. Subida de CV
El candidato puede cargar su currículum en formato PDF o DOCX, con un límite de 5 MB. El sistema almacena el archivo y, opcionalmente, extrae texto para previsualización futura.

### 3. Actualización de perfil
El candidato puede modificar sus datos personales, experiencia laboral y formación sin necesidad de subir un nuevo CV.

### 4. Visualización de currículum
El candidato puede ver una vista previa enriquecida de su CV con los datos extraídos del archivo o los introducidos manualmente. Incluye secciones como experiencia, educación y habilidades.

### 5. Búsqueda de candidatos
Los reclutadores pueden buscar candidatos por palabras clave, habilidades, ubicación o experiencia. Los resultados se muestran en una lista paginada con opciones de filtrado adicional.

### 6. Exportación de CV en PDF
El candidato puede descargar su CV en formato PDF, generado a partir de los datos almacenados en el sistema.

### 7. Integración con LinkedIn
Permitir al candidato importar datos de su perfil de LinkedIn para completar automáticamente el perfil en el sistema.

### 8. Notificaciones automáticas
Envío de notificaciones por correo electrónico o push para recordar al candidato que actualice su CV o cuando se visualice su perfil por un reclutador.

### 9. Cifrado de datos personales
Todos los datos personales identificables (PII) deben estar cifrados en reposo y en tránsito utilizando protocolos robustos (AES-256, TLS 1.2+).

### 10. Tiempo de subida de CV
La operación de carga de un CV de hasta 5 MB debe completarse en menos de 2 segundos para el candidato, excluyendo el tiempo de red del cliente.
