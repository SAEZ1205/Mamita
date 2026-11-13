# Mamita — integración oficial con WhatsApp (propuesta técnica)

## Dos formas distintas
1. **Ahora (manual y gratuita):** En la sección `Mi dinero`, escribir el número WhatsApp de destino y pulsar “Abrir resumen en WhatsApp”. Se abre un chat con el texto preparado; la persona debe pulsar Enviar. No es automático ni requiere API.
2. **Después (automática):** Configurar **WhatsApp Business Platform — Cloud API** y un backend programado que consulte los préstamos que siguen pendientes. Para una alerta al celular de Erika aun con Mamita cerrada, ni `localStorage` ni el HTML estático son suficientes.

## ¿Se puede usar tu número?
- Puedes usar tu propio **número empresarial como remitente** si se registra y habilita legalmente para la Cloud API; no conectes el WhatsApp Messenger personal directamente.
- La madre puede conservar su WhatsApp personal como **destinataria**. Un segundo número de WhatsApp Business puede ser el remitente.
- Es posible que **WhatsApp Business App + Cloud API** compartan el número con la modalidad *coexistence*, pero depende de elegibilidad y del onboarding correcto. Una cuenta Business recién creada **puede no ser elegible**.
- Dos aplicaciones WhatsApp y WhatsApp Business con **dos números distintos** pueden coexistir en el mismo teléfono.

## Prueba inicial con Meta, sin comprar chip
1. Entra a https://developers.facebook.com/ y crea una aplicación con el producto de WhatsApp/Business Messaging.
2. Abre el panel de configuración de WhatsApp; Meta proporciona un número de prueba y un token temporal.
3. Añade y verifica **tu número o el número de tu mamá como destinatario de prueba** desde el panel. No compartas el código SMS de verificación ni el token en chat o repositorio.
4. Desde el panel envía el mensaje de prueba oficial `hello_world` y comprueba que llega.
5. Tras validar esa prueba, decide qué número empresarial definitivo utilizarás. La API de producción puede requerir configuración empresarial, registro de teléfono, plantilla aprobada y facturación.

Documentación oficial: https://developers.facebook.com/documentation/business-messaging/whatsapp/overview

## Para los recordatorios automáticos reales
Arquitectura sugerida:
- APK Mamita: registrar pagos y cuotas en almacenamiento local, sincronizados de forma segura a una base de datos remota privada.
- Servicio programado (p. ej., tarea diaria a las 08:00 hora de Lima): identifica cuotas pendientes, las que vencen hoy y los atrasos; solo envía los datos mínimos y evita mensajes repetidos.
- API Cloud: envía la plantilla aprobada a **un destinatario configurado y que haya dado consentimiento**. Usar nombre/alias y números mínimos, sin documentación sensible.
- Variables de entorno protegidas del servidor: `WHATSAPP_TOKEN`, `WHATSAPP_PHONE_NUMBER_ID`, `MAMITA_ALERT_RECIPIENT`. Nunca insertar estos datos en HTML, APK o commits.
- Supervisión: registrar el éxito/fallo de cada aviso, y mostrar en Mamita el último envío.
- La falta de respuesta por WhatsApp no significa impago: Erika marca los pagos manualmente. La aplicación no debe leer sus chats.

### Sobre tarifas
El uso personal **no exime** de las tarifas de WhatsApp Business Platform. Meta cobra por mensaje entregado según categoría y país, con ciertas ventanas y franquicias para mensajes de servicio. Los recordatorios proactivos normalmente requieren una plantilla; su categorización y aprobación dependen de Meta. La API directa no implica una tarifa adicional de Twilio, aunque Meta puede cobrar por el mensaje.

Fuente de precios oficial: https://whatsappbusiness.com/es-la/products/platform-pricing/
FAQ oficial: https://whatsappbusiness.com/es-la/resources/faq/

**No activar producción ni mensajería automática con nombres reales sin configurar seguridad, consentimiento y costos.**
