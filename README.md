# Mamita · Demo móvil v0.5

Aplicación experimental de control de préstamos para **Erika Leyla Zambrano**, con diseño verde/blanco y tipografía legible. Repositorio privado.

## Probar la interfaz
Descarga `index.html` desde GitHub y ábrelo en Chrome/Edge. Es una demo estática sin build ni dependencias; funciona en el navegador del móvil. No usa servidor ni solicita permisos de WhatsApp.

### Navegación
- **Inicio:** corazón verde animado al abrir y tres botones grandes, sin textos innecesarios: Nuevo préstamo, Mis deudores y Mi dinero.
- **Nuevo préstamo:** escoger **persona nueva** o **persona ya registrada**, nombre/alias del préstamo, avatar ilustrado de mujer/hombre/persona, monto, modalidad y fecha. Una persona nueva recibe código automático `P-0001`, `P-0002`, etc. Si la persona ya existe, es posible registrar un nuevo alias conservando su código. Vista previa con línea horizontal desplazable, puntos diarios, fechas e importes sin solaparse.
- **Mis deudores:** los préstamos son fichas **independientes**, incluso cuando pertenecen a la misma persona. Cada ficha muestra el código `P-XXXX` y, al abrirla, presenta **monto prestado, monto con intereses, total calculado, cobro diario y cronograma** con un botón único de «Registrar pago». La zona de saldos duplicados, historial siempre visible y copiar recordatorio se eliminó para reducir el ruido. Las operaciones de reasignación de clientes y el historial se conservan ocultos en **··· (Opciones del préstamo)**, para no perder su funcionalidad. Se puede ordenar por A–Z, próximo pago (atrasados primero), mayor deuda y más atrasado. Al tocar una ficha se despliega suavemente el monto prestado, el monto con intereses, el total calculado, el cobro diario y una línea de tiempo con una personita amarilla animada que marca la fecha actual. El recorrido es verde hasta hoy y gris después. Los puntos de las cuotas permiten registrar pagos. Tras el vencimiento final, la línea muestra una ventana temporal móvil y no se hace infinita.
- **Mi dinero:** total destacado «Si todos pagaran hoy». Una fila por **código único de persona**, que suma sus préstamos activos. Dentro de esa fila aparecen **líneas temporales separadas** para cada préstamo, con su alias y saldo particular. Se puede ordenar A–Z o por mayor deuda. No se muestran aquí cobros diarios ni desgloses de mora.
- **WhatsApp manual:** permite introducir el número de destino y abrir el resumen prellenado. **No envía mensajes automáticamente.**


## Identificación de personas

La versión 0.4 asocia cada préstamo a un **identificador interno permanente** y muestra un número corto legible (por ejemplo, `P-0001`). Los alias son etiquetas de cada préstamo: **no se usan para unir cuentas automáticamente**. Para registrar un nuevo préstamo de alguien que ya existe, elige «Persona registrada» y selecciona su código. En «Mis deudores» cada préstamo sigue siendo una ficha diferente; en «Mi dinero» aparecen juntos sus saldos, pero con una línea temporal para cada préstamo.

Para deudas ya guardadas antes de la versión 0.4, la primera carga migra los registros previos y los vincula provisionalmente por nombre normalizado, conservando su historial de pagos. **Revisa las coincidencias de nombres tras actualizar**: si una deuda es de otra persona, usa «Vincular» → «Crear otro número» para separarla; si son alias distintos de la misma persona, vincula la deuda al código correcto.

### Refinamiento de interfaz (v0.5)
Se simplificó el detalle desplegable para quitar las secciones «Pagado / Por cobrar», «Persona / Vincular», «Pagos registrados» y «Copiar recordatorio» que estaban ocupando demasiado espacio. El saldo pendiente ya figura en la cabecera de la deuda. El cronograma sigue siendo desplazable y permite tocar cada cuota; el botón «Registrar pago» abre el formulario con la primera cuota todavía pendiente. El movimiento de pagos permanece almacenado y accesible desde las opciones avanzadas. No cambia el cálculo ni la asociación de cuentas.

### Visual móvil
La escala temporal utiliza separación fija en píxeles por día y desplazamiento horizontal en pantallas pequeñas para evitar superponer fechas, importes y estados. Al superar el último vencimiento muestra una ventana temporal cercana al día actual. La animación es decorativa; los movimientos reducidos se respetan cuando así lo pide el dispositivo.


### Cálculos demostrativos
- Mensual: capital + 30 % pactado, con vencimiento a 30 días; recargo simulado de 2 % del capital por día de atraso.
- Semanal: capital + 20 % pactado, cuatro cuotas a 7, 14, 21 y 28 días; recargo simulado de 1,3 % del capital por cada día de atraso de cada cuota.
- Los vencimientos y los días de mora se calculan **independientemente por cuota**. Los pagos adelantados, parciales y el recargo abonado se registran separadamente.

**Precaución legal:** Estas tasas se conservan únicamente como ejemplo pedido por el usuario. Antes de aplicar cobros reales deben ajustarse a la normativa peruana y verificarse los topes de interés/mora aplicables.

### Persistencia y limitaciones
Los datos ficticios se cargan al primer uso. Los registros de prueba, las fichas de clientes y los vínculos se almacenan juntos en `localStorage` del mismo navegador. **No hay cuenta, respaldos, sincronización, API de WhatsApp ni notificaciones programadas.** No usar con datos personales reales ni como contabilidad definitiva. El botón de restablecer elimina los registros locales de prueba.

Para avisos automáticos aun con la APK cerrada se necesitará una base de datos protegida y un proceso programado del lado del servidor. Los tokens de Meta **nunca** deben estar dentro de `index.html` ni en GitHub. Consulta [WHATSAPP.md](WHATSAPP.md).

### Publicación
El código puede importarse como sitio estático a un hosting que admita `index.html`. Vercel rechazó la creación automática del proyecto con un error 403 de permisos de la conexión; **la conexión del hosting actual con este repositorio no ha sido verificada desde aquí**. El usuario ha compartido una URL de AWS Amplify, pero no se pudo acceder a su contenido para confirmar la versión publicada.
