# Descripcion



Actúa como un CTO, Arquitecto de Software Principal y Desarrollador Full-Stack Senior experto en plataformas SaaS de alta concurrencia, sistemas en tiempo real y hardware mobile (Bluetooth Low Energy / BLE).

Quiero clonar y mejorar el sistema de la plataforma "FourVenues" (software de gestión de ocio nocturno, venta de entradas y reservados VIP). Mi plataforma incluirá una ventaja competitiva clave: automatización de accesos por proximidad Bluetooth (BLE) y marketing de proximidad en tiempo real.

Por favor, genera una especificación de arquitectura detallada y el código base estructurado, separando el ecosistema en tres partes (Backend, Software de Usuario y Software de Local), implementando la pasarela de pagos con Stripe.

---

### TECH STACK SUGERIDO (Adaptable si propones algo más óptimo)
- Backend: Node.js (TypeScript) con Express/Fastify o NestJS.
- Bases de datos: PostgreSQL (para transacciones y consistencia) + Redis (para caché, colas de entradas y WebSockets en tiempo real).
- Mobile: React Native o Flutter (con librerías nativas BLE como react-native-ble-manager / flutter_blue_plus).

---

## PARTE 1: BACKEND CENTRALIZADO (API & TIEMPO REAL)
Diseña el backend arquitectónico con soporte para:
1. WebSockets / Socket.io: Para actualizar la lista de puerta del local al milisegundo cuando un usuario entra o compra.
2. Generación de Tokens Dinámicos (TOTP): Mecanismo que genere un token Bluetooth cifrado que cambie cada 30 segundos vinculado al ID de la entrada para evitar fraudes (capturas de pantalla o clonación de señal).
3. Motor de Proximidad: Endpoint que reciba el ID de un Beacon detectado por un móvil y devuelva ofertas push personalizadas según la disponibilidad del local (ej: Upgrades a VIP).

---

## PARTE 2: SOFTWARE DEL USUARIO (App Móvil / Web App Cliente)
Genera la lógica y estructura para la aplicación orientada al cliente final:
1. Módulo Bluetooth (Emisor/Peripheral): Código o lógica nativa para que la app actúe como un Beacon/Peripheral cuando el usuario está cerca del local (Geofencing). Debe emitir el token dinámico de la entrada (TOTP) incluso optimizando el comportamiento en segundo plano (Background Mode).
2. Flujo de Compra y Registro: Interfaz fluida para ver eventos, seleccionar entradas generales o seleccionar mesas VIP en un mapa interactivo.
3. KYC Integrado (Mock/Estructura): Flag `age_verified` (Booleano) y lógica para comprobar si cumple la restricción +21 del evento antes de emitir la señal Bluetooth de acceso.

---

## PARTE 3: SOFTWARE DEL LOCAL (Panel Web de Gestión & App de Porteros)
Genera la lógica y estructura para los dueños del local, RRPP y porteros:
1. App del Portero (Receptor/Central BLE): Lógica de escaneo continuo de señales Bluetooth en la fila. Debe filtrar dispositivos por potencia de señal (RSSI) para listar arriba a los que están a <2 metros. La interfaz debe listar: Nombre, Foto (antifraude), Tipo de Entrada (General o Reservado VIP) y botón de "Validar" o "Validar Grupo Completo" en un solo clic vía WebSockets.
2. Panel de Administración del Local: Dashboard para crear eventos, asignar zonas de reservados VIP, configurar precios por tramos, asignar Beacons publicitarios físicos a la fachada y ver analíticas de aforo en tiempo real.

---

## PARTE 4: SISTEMA DE COBROS CON STRIPE (Tarjeta de Crédito)
Implementa el flujo completo y seguro de pagos de extremo a extremo:
1. Backend (Server-Side): 
   - Endpoint `POST /api/payments/create-intent`: Crea un `PaymentIntent` de Stripe calculando el precio real de la entrada o el depósito de la mesa VIP en el servidor (para evitar manipulaciones del cliente).
   - Endpoint `POST /api/payments/webhook`: Escucha eventos nativos de Stripe (`payment_intent.succeeded`). Al confirmarse, genera automáticamente la entrada en la base de datos, asigna el token BLE y dispara la notificación al usuario.
2. Frontend Cliente (Client-Side):
   - Integración de Stripe Elements o el SDK nativo de Stripe móvil para capturar de forma segura los datos de la tarjeta de crédito y confirmar el pago con el `client_secret`.

---

### FORMATO DE RESPUESTA REQUERIDO
Por favor, estructura tu respuesta de la siguiente manera:
1. Diagrama de arquitectura del flujo de datos (Backend -> Cliente -> Portero -> Stripe).
2. Código limpio, modular y comentado para el backend (Estructura de carpetas, endpoints críticos y WebSockets).
3. Código/Lógica para el Software de Usuario (Módulo BLE Emisor y Pasarela Stripe).
4. Código/Lógica para el Software del Local (Módulo BLE Escáner del Portero y UI en tiempo real).

Usa TypeScript para los ejemplos de código y asegúrate de explicar cómo manejar de forma segura las claves secretas de Stripe y las restricciones de BLE en segundo plano.