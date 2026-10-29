# 🚗 Gestor de Vehículos

Aplicación de escritorio en **Java (Swing)** para llevar el control de una flota de vehículos: sus kilómetros, su historial de reparaciones y los **avisos automáticos de mantenimiento**.

Proyecto final de **Programación** de 1.º de DAM.

<p align="center">
  <img src="docs/captura-ventana-principal.png" alt="Ventana principal del gestor de vehículos" width="600" />
</p>

## ✨ Funcionalidades

- ➕ **Añadir y eliminar vehículos** (marca, modelo, matrícula, tipo y kilómetros)
- 🔧 **Registrar reparaciones** de cada vehículo (tipo, fecha, kilómetros y coste)
- 🔄 **Actualizar los kilómetros** de un vehículo
- ⚠️ **Aviso de revisión:** la lista marca con `NECESITA REVISIÓN` los vehículos que la requieren
- 💾 **Guardado automático** en un fichero de texto al cerrar la aplicación, y carga al abrirla
- 🛡️ Validación de datos: avisa si los kilómetros o el coste no son números, o si el tipo o la fecha son incorrectos

## 🧠 Cómo decide si un vehículo necesita revisión

- **Sin reparaciones registradas:** se compara con un límite según el tipo de vehículo.

  | Tipo | Límite |
  |---|---|
  | Coche | 15 000 km |
  | Moto | 6 000 km |
  | Furgoneta | 20 000 km |
  | Camión | 30 000 km |

- **Con reparaciones:** necesita revisión cuando los kilómetros actuales superan los de la **última reparación** más el intervalo de ese tipo de reparación.

  | Reparación | Intervalo |
  |---|---|
  | Cambio de aceite | 10 000 km |
  | Cambio de filtro de aire | 20 000 km |
  | Pastillas de freno | 40 000 km |
  | Otros | 15 000 km |

## 🛠️ Conceptos de programación aplicados

- **Programación orientada a objetos:** clases `Vehiculo`, `Reparacion` y `GestionVehiculos`
- **Interfaces:** `AvisoMantenimiento`, implementada por `Vehiculo`
- **Enumerados con atributos:** `TipoVehiculo` y `TipoReparacion` (con su intervalo de km)
- **Colecciones y Streams:** búsqueda por matrícula, ordenación por kilómetros, recuento de vehículos con revisión pendiente
- **Ficheros:** lectura y escritura con `BufferedReader` y `BufferedWriter`
- **Interfaz gráfica con Swing:** `JFrame`, `JList`, `JOptionPane` y manejo de eventos
- **Gestión de excepciones** ante datos incorrectos del usuario

## 📁 Estructura

```
gestor-vehiculos-java/
├── src/ProyectoFinal/
│   ├── Main.java                  # Punto de entrada
│   ├── Vehiculo.java              # Datos del vehículo y lógica de revisión
│   ├── Reparacion.java            # Reparación realizada a un vehículo
│   ├── GestionVehiculos.java      # Lista de vehículos, búsquedas y guardado en fichero
│   ├── AvisoMantenimiento.java    # Interfaz de aviso
│   ├── TipoVehiculo.java          # Enum: COCHE, MOTO, FURGONETA, CAMION
│   ├── TipoReparacion.java        # Enum con el intervalo de km de cada reparación
│   ├── VentanaPpal.java           # Ventana principal
│   └── VentanaReparaciones.java   # Ventana del historial de reparaciones
├── datos-ejemplo/vehiculos.txt    # Datos ficticios para probar la aplicación
└── docs/                          # Capturas
```

## 🚀 Cómo ejecutarlo

Necesitas tener instalado el **JDK 11 o superior** ([descargar](https://adoptium.net/)).

```bash
# 1. Clonar el repositorio
git clone https://github.com/Jur-Nov/gestor-vehiculos-java.git
cd gestor-vehiculos-java

# 2. (Opcional) Copiar los datos de ejemplo para ver la aplicación con vehículos
cp datos-ejemplo/vehiculos.txt .

# 3. Compilar
mkdir bin
javac -encoding UTF-8 -d bin src/ProyectoFinal/*.java

# 4. Ejecutar (desde la carpeta raíz, para que encuentre vehiculos.txt)
java -cp bin ProyectoFinal.Main
```

> En Windows, para copiar el fichero de ejemplo usa `copy datos-ejemplo\vehiculos.txt .`

Si no existe `vehiculos.txt`, la aplicación arranca vacía y lo crea al cerrarse.

## 💾 Formato del fichero de datos

Un fichero de texto donde cada línea `V` es un vehículo y las líneas `R` que la siguen son sus reparaciones:

```
V,marca,modelo,matrícula,TIPO,kilómetros
R,TIPO_REPARACION,fecha(AAAA-MM-DD),kilómetros,coste
```

## 🔮 Posibles mejoras

- Sustituir los cuadros de diálogo por formularios con desplegables para el tipo de vehículo y de reparación
- Guardar los datos en una **base de datos** en lugar de un fichero de texto
- Impedir matrículas duplicadas y validar su formato
- Mostrar el coste total de reparaciones por vehículo
- Ordenar y filtrar la lista desde la interfaz

## 👤 Autor

**Jur-Nov** · Estudiante de DAM · [GitHub](https://github.com/Jur-Nov)
