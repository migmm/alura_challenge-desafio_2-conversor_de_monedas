
# CHALLENGE -DESAFÍO 2 - JAVA

<p align="center">
    <img src="https://github.com/migmm/alura_challenge-desafio_1-logica/blob/main/assets/aluraoracle.png" alt="Logo"/>
</p>

## Conversor de monedas

Este proyecto es un **conversor de monedas** desarrollado en **Java**. Permite a los usuarios convertir entre diferentes divisas utilizando datos en tiempo real obtenidos de la API de **ExchangeRate-API**. El programa incluye funcionalidades adicionales como ver las tasas de cambio de diferentes monedas y guardar las conversiones realizadas en un archivo de texto para referencia futura.

### Funcionalidades

1. **Convertir Monedas**: Permite al usuario convertir un importe de una moneda a otra.
2. **Ver Cotizaciones**: Muestra las tasas de compra y venta para una moneda seleccionada.
3. **Ver Conversiones Anteriores**: Muestra las conversiones guardadas previamente en un archivo de texto.
4. **Guardar Conversiones**: Cada vez que se realiza una conversión, se guarda en un archivo `conversiones.txt`.

### Requisitos

- **Java 22** o superior
- **Maven**
- Dependencias de terceros:
  - `Gson`: Para parsear los datos JSON.
  - `ExchangeRate-API`: Para obtener las tasas de cambio.

### Estructura del Proyecto

```bash
.
├── src
│   ├── main
│   │   ├── java
│   │   │   └── org
│   │   │       └── conversor_monedas
│   │   │           ├── ClienteHTTP.java
│   │   │           ├── Configuracion.java
│   │   │           ├── Main.java
│   │   │           └── Moneda.java
│   │   └── resources
│   │       └── application.properties
├── conversiones.txt
└── pom.xml

```

### Archivos Principales

    Main.java: Contiene el flujo principal del programa y maneja el menú interactivo.
    ClienteHTTP.java: Clase encargada de realizar las solicitudes HTTP a la API y obtener los datos JSON de las tasas de cambio.
    Configuracion.java: Lee el archivo application.properties para obtener la clave API desde un archivo de configuración.
    Moneda.java: Clase que representa una conversión de moneda con métodos para formatear los resultados.
    application.properties: Archivo de configuración donde se almacena la clave de la API (api.exchangerate.key).

### Dependencias

El proyecto utiliza Maven para la gestión de dependencias. Las principales dependencias son:


<dependencies>
    <dependency>
        <groupId>com.google.code.gson</groupId>
        <artifactId>gson</artifactId>
        <version>2.8.9</version>
    </dependency>
</dependencies>

Esta dependencia se utiliza para parsear los datos JSON devueltos por la API de ExchangeRate.


### Configuración

1. Clave API

Debes configurar tu propia clave de la API de ExchangeRate para obtener las tasas de cambio. Para ello:

    Regístrate en ExchangeRate-API y obtén una API key.
    Coloca la clave en el archivo application.properties que se encuentra en src/main/resources.

El archivo application.properties debe verse así:

properties

api.exchangerate.key=TU_API_KEY_AQUI

2. Ejecutar el Proyecto

Para ejecutar el proyecto, sigue los siguientes pasos:

    Clona este repositorio.

    Asegúrate de tener Maven instalado.

    Ejecuta el siguiente comando para compilar el proyecto:

    ```bash

mvn clean install
```
Luego, ejecuta la aplicación con:

```bash

    mvn exec:java -Dexec.mainClass="org.conversor_monedas.Main"
```

### Uso del Programa

El menú interactivo te permitirá seleccionar entre las diferentes opciones disponibles:

    Convertir un importe:
        Selecciona la moneda de origen.
        Selecciona la moneda destino.
        Introduce el importe a convertir.

    El programa mostrará el resultado de la conversión con las tasas de compra y venta, y guardará esta conversión en conversiones.txt.

    Ver valores de cotización:
        Selecciona una moneda para ver su tasa de compra y venta en relación a la moneda base seleccionada.

    Ver conversiones anteriores:
        Muestra las conversiones guardadas en conversiones.txt.

    Salir:
        Finaliza la ejecución del programa.

### Ejemplo de Ejecución

```bash

==================================
====== Conversor de Monedas ======
==================================

1. Convertir un importe
2. Ver valores de cotización
3. Ver conversiones anteriores
4. Salir

Seleccioná la moneda base:

1. USD       5. AUD
2. EUR       6. CAD
3. JPY       7. ARS
4. GBP       8. BRL
Elegí la moneda base: 1

Seleccioná la moneda a la que deseas convertir:
1. USD       5. AUD
2. EUR       6. CAD
3. JPY       7. ARS
4. GBP       8. BRL
Elegí la moneda destino: 2

Introducí el importe a convertir: 100

Resultado de Conversión:
| Moneda     | Importe Base   | Valor de Compra | Valor de Venta  |
|------------|----------------|-----------------|-----------------|
| EUR        | 100.00         | 85.00           | 101.00          |

```

### Detalles Técnicos

    Gson: Se utiliza para parsear la respuesta en formato JSON obtenida de la API.

    Ejemplo de parseo:

```bash

JsonObject jsonObject = JsonParser.parseString(datosJSON).getAsJsonObject();
JsonObject rates = jsonObject.getAsJsonObject("conversion_rates");
```

Archivos: El proyecto utiliza la clase BufferedWriter para guardar las conversiones en un archivo de texto y BufferedReader para leer dichas conversiones.

Ejemplo de guardado de conversiones:

```bash

    try (BufferedWriter writer = new BufferedWriter(new FileWriter(ARCHIVO_CONVERSIONES, true))) {
        writer.write(conversion.formatoMoneda());
        writer.newLine();
    }

```

### ¿Qué se Usó y Cómo se Aplicó?

1. **Java**: El lenguaje principal utilizado para todo el desarrollo.
2. **Maven**: Para gestionar las dependencias (como Gson) y la compilación del proyecto.
3. **Gson**: Para parsear las respuestas JSON obtenidas de la API de ExchangeRate.
4. **ExchangeRate-API**: API utilizada para obtener las tasas de cambio en tiempo real.
5. **Archivo `application.properties`**: Se utilizó para almacenar la clave de la API, separando la configuración sensible del código.
6. **Archivos**: Se implementaron clases que escriben y leen datos en un archivo de texto (`conversiones.txt`), lo que permite guardar y ver conversiones anteriores.
7. **Menú interactivo**: Presenta un menú que guía al usuario a través de diferentes opciones, como realizar conversiones, ver tasas de cambio, y consultar conversiones pasadas.

