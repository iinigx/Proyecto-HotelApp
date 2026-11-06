🏨 HotelApp — Sistema de reservas

Aplicación de escritorio desarrollada con JavaFX para gestionar la información del Hotel Sol (4 estrellas, Madrid). Lee los datos de habitaciones y reservas desde un fichero XML y los muestra en una interfaz con dos pestañas: consulta de habitaciones e informes de reservas para el gerente.

✨ Funcionalidades
Pestaña «Habitaciones»
Listado de todas las habitaciones con su tipo, capacidad, precio por noche y estado.
Búsqueda por número de habitación con respuesta visual por colores:
🟢 Disponible
🔴 Ocupada
🟣 La habitación no existe
🟠 No se ha introducido ningún número
Pestaña «Informes de reservas»
Tabla con código, estado, cliente, habitación, fechas de entrada y salida y número de personas.
Filtros combinables por estado (Todos, Confirmada, Finalizada, Cancelada, Pendiente) y por mes (Todos los meses, Octubre 2026, Noviembre 2026).
Totales que se recalculan al aplicar cada filtro: total de reservas y desglose por estado.
🛠️ Tecnologías
Tecnología	Versión	Uso
Java	21	Lenguaje principal
JavaFX (controls + fxml)	21.0.4	Interfaz gráfica
Maven	–	Gestión de dependencias y ejecución
javafx-maven-plugin	0.0.8	Lanzar la app con mvn javafx:run
DOM (javax.xml.parsers)	–	Lectura del XML
📁 Estructura del proyecto
HotelApp_Parte1/
├── pom.xml
├── .vscode/
│   └── launch.json              # Configuración de ejecución en VS Code
└── src/main/
    ├── java/
    │   ├── Main.java            # Punto de entrada: carga la vista FXML
    │   ├── HotelController.java # Controlador: lectura del XML, búsqueda y filtros
    │   └── Reserva.java         # Modelo de datos de una reserva
    └── resources/
        ├── vista.fxml           # Definición de la interfaz
        └── reservas.xml         # Datos del hotel (habitaciones y reservas)
🧩 Arquitectura

Sigue el patrón vista – controlador – modelo habitual en JavaFX:

Vista (vista.fxml): declara los controles (TabPane, ListView, TableView, ComboBox, etiquetas…) y enlaza los eventos con el controlador.
Controlador (HotelController): en initialize() carga el XML, rellena la lista de habitaciones y configura la tabla y los filtros del informe.
Modelo (Reserva): clase inmutable con los datos de cada reserva y métodos auxiliares (getClienteCompleto(), getEstadoFormateado(), parseFecha()).
🗂️ Datos de ejemplo (reservas.xml)

El XML contiene los datos del hotel (nombre, ciudad, dirección y teléfono), 30 habitaciones y 30 reservas:

Habitaciones	Cantidad		Reservas	Cantidad
Ocupadas	10		Confirmadas	15
Disponibles	17		Finalizadas	5
En mantenimiento	3		Canceladas	5
			Pendientes	5

Cada habitación incluye número, planta, tipo (Individual, Doble, Familiar, Suite), capacidad, precio por noche, vista y accesibilidad. Cada reserva incluye código, estado, datos del cliente, habitación, fechas, personas y observaciones.

🚀 Cómo ejecutarlo
Requisitos
JDK 21 o superior
Maven 3.6+ (o un IDE con soporte Maven)
Con Maven (recomendado)
bash
cd HotelApp_Parte1
mvn javafx:run
Desde VS Code

El fichero .vscode/launch.json incluye una configuración «Launch Main» que usa una ruta local al SDK de JavaFX. Si lo ejecutas desde VS Code, edita el parámetro --module-path para que apunte a la carpeta lib de tu SDK de JavaFX.

Desde otro IDE (IntelliJ, Eclipse, NetBeans)

Importa el proyecto como proyecto Maven y ejecuta la clase Main.

📝 Notas y posibles mejoras
Los meses del filtro (Octubre y Noviembre 2026) están fijados en el código; se podrían generar dinámicamente a partir de las fechas de las reservas.
La lista de habitaciones se guarda en un HashMap, por lo que no se garantiza el orden; usar un TreeMap las mostraría ordenadas por número.
Se podrían añadir altas, modificaciones y cancelaciones de reservas con escritura de vuelta al XML.
Exportación del informe a PDF o CSV.
👤 Autor

Iñigo Rojo Crespo — 2º DAM
