# Mamita · Demo móvil v0.2

Aplicación experimental de control de préstamos para **Erika Leyla Zambrano**, con diseño verde/blanco y tipografía legible. Repositorio privado.

## Probar la interfaz
Descarga `index.html` desde GitHub y ábrelo en Chrome/Edge. Es una demo estática sin build ni dependencias; funciona en el navegador del móvil. No usa servidor ni solicita permisos de WhatsApp.

### Navegación
- **Inicio:** tres botones grandes: Nuevo préstamo, Mis deudores y Mi dinero.
- **Nuevo préstamo:** alias, icono opcional (hombre/mujer/neutro), importe, modalidad, fecha de entrega y vista previa con línea de tiempo horizontal.
- **Mis deudores:** nombres en orden alfabético; tocar una fila despliega los importes y cada cuota en un cronograma horizontal con fecha, estado, mora y registro de abonos.
- **Mi dinero:** saldo total por cobrar si todos pagaran en la fecha actual de Perú; muestra importes por persona y una barra cronológica del inicio al vencimiento final.
- **WhatsApp manual:** permite introducir el número de destino y abrir el resumen prellenado. **No envía mensajes automáticamente.**

### Cálculos demostrativos
- Mensual: capital + 30 % pactado, con vencimiento a 30 días; recargo simulado de 2 % del capital por día de atraso.
- Semanal: capital + 20 % pactado, cuatro cuotas a 7, 14, 21 y 28 días; recargo simulado de 1,3 % del capital por cada día de atraso de cada cuota.
- Los vencimientos y los días de mora se calculan **independientemente por cuota**. Los pagos adelantados, parciales y el recargo abonado se registran separadamente.

**Precaución legal:** Estas tasas se conservan únicamente como ejemplo pedido por el usuario. Antes de aplicar cobros reales deben ajustarse a la normativa peruana y verificarse los topes de interés/mora aplicables.

### Persistencia y limitaciones
Los datos ficticios se cargan al primer uso. Los registros de prueba se almacenan solo en `localStorage` del mismo navegador. **No hay cuenta, respaldos, sincronización, API de WhatsApp ni notificaciones programadas.** No usar con datos personales reales ni como contabilidad definitiva. El botón de restablecer elimina los registros locales de prueba.

Para avisos automáticos aun con la APK cerrada se necesitará una base de datos protegida y un proceso programado del lado del servidor. Los tokens de Meta **nunca** deben estar dentro de `index.html` ni en GitHub. Consulta [WHATSAPP.md](WHATSAPP.md).

### Publicación
El código puede importarse como sitio estático a un hosting que admita `index.html`. Vercel rechazó la creación automática del proyecto con un error 403 de permisos de la conexión; **no hay enlace de despliegue confirmado**.
