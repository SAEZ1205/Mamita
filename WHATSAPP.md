# Avisos automáticos de Mamita — decisión de integración (13/11/2026)

## Advertencia: WhatsApp Business no es una integración autorizada para el caso de Mamita

La política de mensajes de **WhatsApp Business** vigente desde el 23 de septiembre de 2026 **prohíbe el uso de sus servicios para préstamos entre particulares y cobro de deudas**, aun cuando se utilice la API oficial, Twilio u otro intermediario. Este proyecto gestiona préstamos personales y recordatorios de cuotas vencidas; **no implementaremos recordatorios de cobro automatizados mediante WhatsApp Business API ni números destinados a eludir esta restricción**.

Política oficial: https://whatsappbusiness.com/es-la/policy/

Comprar otra SIM o configurar WhatsApp Business **no resuelve esta prohibición**. La versión anterior de esta guía describía cómo conectar la Cloud API de Meta, pero no había contemplado esta restricción específica; esa recomendación queda sustituida por este documento.

## Soluciones propuestas

### 1. Preferida: bot privado de Telegram
- Instalar Telegram en el teléfono de Erika (con su número actual, sin comprar otra SIM).
- Crear un bot privado con @BotFather, abrirlo desde el Telegram de Erika y pulsar `Iniciar` / `/start`.
- Alojaremos la clave privada del bot en el **servidor**, nunca en HTML, APK ni commits.
- Una tarea programada consultará cuotas aún pendientes en una base de datos privada, calculará fechas según `America/Lima`, y enviará un resumen diario al chat autorizado de Erika.
- Se deberá evitar revelar datos personales completos en mensajes. Usar alias, importe total, fecha y número de cuota, siempre sujeto a consentimiento y normativa aplicable.
- Es necesario respaldar/sincronizar datos: el almacenamiento actual `localStorage` del demo solo vive en el navegador y un servidor externo no puede leerlo.
- Este servicio no está instalado ni activado todavía.

La API de bots de Telegram es gratuita para uso normal:
https://core.telegram.org/bots
https://core.telegram.org/bots/api
https://core.telegram.org/api

### 2. Alternativa sin otra app: notificaciones Android reforzadas
Crear una APK Android nativa con resumen diario, notificaciones con mayor prioridad y pantalla de pendientes. La entrega a la hora exacta puede depender de permisos de alarmas y restricciones del fabricante; Android 14 deniega por defecto permisos de alarmas exactas a muchas apps nuevas:
https://developer.android.com/about/versions/14/changes/schedule-exact-alarms

### 3. Mensaje manual en WhatsApp
La demo contiene un enlace de WhatsApp `wa.me` para abrir el texto de un resumen y que Erika decida enviarlo manualmente. No es una notificación automática y no debe usarse para automatizar cobros. Mantener su uso de acuerdo con las condiciones del servicio.

## Arquitectura para instalación real
1. Datos de préstamos y pagos en una base de datos privada cifrada y con copias de seguridad.
2. APK que registra cada abono con fecha y sincroniza los estados con el servidor.
3. Proceso programado por la mañana hora Perú con control de duplicados, logs y reintentos.
4. Bot privado de Telegram o notificación Android: solo la madre será destinataria autorizada.
5. Aplicar las tasas legales de préstamo y mora vigentes en Perú antes de desplegar la solución para cobros reales.

**Estado actual:** únicamente diseño HTML estático de Mamita, sin backend, APK ni envíos automáticos.
