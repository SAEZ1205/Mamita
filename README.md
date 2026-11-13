# Mamita — demo de control de préstamos

Demostración estática para **Erika Leyla Zambrano**. Los datos iniciales son **ficticios** y el repositorio debe mantenerse privado.

## Cómo probarlo
1. Abrir `index.html` en el navegador (se puede descargar desde GitHub y hacer doble clic). No requiere instalar dependencias ni un servidor.
2. En **Nuevo préstamo**, indicar alias, monto, fecha y modalidad mensual o semanal. La vista previa muestra el interés y las fechas exactas.
3. En **Mis deudores**, abrir una ficha, ver el cronograma independiente de cada cuota y registrar un pago completo, parcial, anticipado o de mora.
4. Los cambios se guardan en `localStorage` del navegador. **Restablecer datos de prueba** recupera los clientes ficticios.

## Cálculos (solo simulación)
- **Mensual:** 30 % sobre el monto original, un vencimiento a 30 días y un recargo simulado de 2 % diario después del vencimiento.
- **Semanal:** 20 % sobre el monto original, cuatro cuotas a los días 7, 14, 21 y 28. Recargo simulado de 1,3 % del monto original por día **por cuota vencida e impaga**.
- Cada cuota lleva su propia fecha y cálculo de mora. Una cuota completamente abonada deja de generar días de atraso. El recargo ya acumulado permanece hasta que se anote su pago.

**ATENCIÓN:** Las tasas de este demo son las propuestas para ilustrar las operaciones y deben contrastarse y adecuarse a los topes legales aplicables en Perú antes de realizar cobros reales.

## Alcance y privacidad
- Es una página HTML/CSS/JavaScript sin backend.
- No accede a contactos, SMS ni WhatsApp, y **no envía mensajes automáticos**.
- No usa cuentas ni sincronización en la nube; no debe utilizarse como registro definitivo de préstamos reales.
- No hay respaldos automáticos: cambiar de navegador, borrar los datos de sitio o perder el celular puede borrar los registros.
- Antes de entregar la APK real faltan almacenamiento seguro, copias de seguridad, pruebas con pagos reales y avisos programados vía servicio externo/WhatsApp API.

## Publicación
El proyecto puede desplegarse como **sitio estático** en Vercel importando `SAEZ1205/Mamita` y seleccionando la carpeta raíz. No requiere build ni framework. Mantener el repositorio privado. El sitio de demostración solo debe usarse con nombres ficticios.
