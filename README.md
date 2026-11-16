# Mamita · Demo móvil v0.3

Aplicación experimental de control de préstamos para **Erika Leyla Zambrano**, con diseño verde/blanco y tipografía legible. Repositorio privado.

## Probar la interfaz
Descarga `index.html` desde GitHub y ábrelo en Chrome/Edge. Es una demo estática sin build ni dependencias; funciona en el navegador del móvil. No usa servidor ni solicita permisos de WhatsApp.

### Navegación
- **Inicio:** corazón verde animado al abrir y tres botones grandes, sin textos innecesarios: Nuevo préstamo, Mis deudores y Mi dinero.
- **Nuevo préstamo:** alias, icono opcional (hombre/mujer/neutro), importe, modalidad y fecha. Vista previa con una línea horizontal real, puntos diarios y estaciones con fecha e importe; se destaca el cobro por día de atraso.
- **Mis deudores:** los préstamos son fichas **independientes**, incluso cuando dos fichas tienen el mismo nombre. Se puede ordenar por A–Z, próximo pago (atrasados primero), mayor deuda y más atrasado. Al tocar una ficha se despliega suavemente el monto prestado, el monto con intereses, el total calculado, el cobro diario y una línea de tiempo con una personita amarilla animada que marca la fecha actual. El recorrido es verde hasta hoy y gris después. Los puntos de las cuotas permiten registrar pagos. Tras el vencimiento final, la línea muestra una ventana temporal móvil y no se hace infinita.
- **Mi dinero:** solo el total destacado «Si todos pagaran hoy», una lista de personas y una línea de tiempo resumida por cada una. Los préstamos activos del **mismo nombre/alias normalizado** se agrupan en una única fila, sumando lo que debe esa persona. Se puede ordenar A–Z o por mayor deuda. No se muestran aquí cobros diarios ni desgloses de mora.
- **WhatsApp manual:** permite introducir el número de destino y abrir el resumen prellenado. **No envía mensajes automáticamente.**


## Regla de agrupación provisional
En esta **demo**, los préstamos se agrupan en «Mi dinero» por coincidencia del nombre o alias sin distinguir mayúsculas ni espacios repetidos. Si dos personas diferentes tienen el mismo nombre, aparecerán juntas indebidamente. **Antes de usar la APK en operaciones reales, reemplazaremos esta agrupación por un identificador único de cliente y selección explícita de personas ya registradas.**

Para comprobar la función de agrupación, crea dos préstamos con el mismo alias y abre «Mi dinero»: la lista mostrará una persona con el importe agregado mientras «Mis deudores» conserva dos fichas separadas.

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
