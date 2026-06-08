# Requirements

**Total:** 7 requirements

1. **[MUST]** FR-001 — Emisión de token BLE dinámico (TOTP) desde app de usuario
   La aplicación móvil genera un token Bluetooth basado en TOTP que cambia cada 30 segundos, vinculado a la entrada adquirida. El token se emite en modo periférico BLE al detectar el geofence del local, incluso en segundo plano. No se emite si el usuario no tiene la verificación de edad superada.
2. **[MUST]** FR-002 — Escáner BLE del portero con filtrado RSSI y validación
   La app del portero escanea dispositivos BLE cercanos, filtra aquellos que emitan tokens válidos y los ordena por proximidad usando el RSSI (umbral <-50 dBm para <2 m). Muestra nombre, foto, tipo de entrada y permite validar entrada individual o de grupo.
3. **[MUST]** FR-003 — Validación en tiempo real y actualización de puerta vía WebSockets
   El backend notifica en tiempo real a la app del portero y al panel de administración cada vez que una entrada es validada, actualizando el aforo del local al instante. Utiliza Socket.io para latencias inferiores a 200 ms.
4. **[MUST]** FR-004 — Procesamiento de pagos con Stripe (PaymentIntent y webhook)
   El backend expone un endpoint para crear un PaymentIntent de Stripe con el importe calculado en servidor, y escucha el webhook payment_intent.succeeded para generar la entrada, asignar el token BLE y notificar al usuario.
5. **[SHOULD]** FR-005 — Panel de administración del local (eventos, zonas VIP y analíticas)
   Interfaz web para que el gestor pueda crear eventos, definir zonas de reservados VIP, configurar precios, asignar beacons publicitarios y visualizar analíticas de aforo en tiempo real.
6. **[SHOULD]** FR-006 — Verificación de edad (KYC) para cumplimiento de restricciones +21
   La app solicita al usuario verificar su edad mediante carga de documento o autodeclaración, almacenando un flag age_verified en el backend. Si no se cumple la restricción, se bloquea la emisión de la señal BLE de acceso.
7. **[COULD]** FR-007 — Motor de proximidad para ofertas push personalizadas
   Al detectar un beacon publicitario (ID) desde la app del usuario, el backend consulta la disponibilidad del local y devuelve una oferta (p. ej., upgrade a VIP) que se envía como notificación push si el usuario ha dado su consentimiento.
