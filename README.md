# Parte 1 - Datos de mercado

Escriba un programa Java que recupere un archivo de datos a través de HTTP desde una URL dada y emite otro archivo con un subconjunto de la información de la primera. Debería tomar un parámetro de línea de comando, el URL del archivo de entrada.

El archivo de entrada está en (https://raw.githubusercontent.com/mlennard-utn/tp_avanzado/master/mercado.json), una lista JSON de valores negociados públicamente con algunos metadatos para cada uno.

El archivo de salida tiene un registro más simple para cada uno, con ticker, price e ISIN (etiquetado como `id` en los datos de origen). El campo `price` no debe tener ceros al final. El ticker es opcional en el archivo de entrada y dichos registros deben incluirse en el archivo de salida, con un campo de cotización establecido en nulo.

Por ejemplo, registro de entrada
`` `
  {
    "currency: USD",
    "ticker": "H",
    "exchange": "USNYSE",
    "id": "US4485791028",
    "price": 51.3100,
    "name": "Hyatt Hotels Corporation"
  }
`` `

Lista como salida

`` `
  {
    "ticker": "H",
    "price": 51.31,
    "isin": "US4485791028"
  }
`` `

Ejemplo de ejecución del programa
`` `
$ ./myprogram https://raw.githubusercontent.com/mlennard-utn/tp_avanzado/master/mercado.json
[
  {
    "ticker": "ABC",
    "price": 10.5,
    "isin": "US1234567890"
  },
  {
    "ticker": "BBB",
    "price": 400,
    "isin": "US0987654321"
  },
  ...
]
`` `
---

# Parte 2 - Alertas de Préstamo

Escriba un programa Java que tome el archivo de datos de mercado de la primera parte, más otro archivo que enumere las cuentas de clientes de préstamos.

Los detalles de la cuenta tienen dos partes: la cantidad pendiente del préstamo y la cartera que es la garantía, asegurando este préstamo. La cartera es una lista de los valores que cotiza en bolsa que contiene, identificados por el ISIN, y la cantidad de cada uno de ellos.

El programa comparará el valor total de la cartera con el monto pendiente del préstamo y generará un archivo con los detalles de las cuentas en las que el préstamo no está completamente garantizado porque el monto del préstamo es mayor que el valor de la cartera. Cuando este es el caso, se debe incluir un registro con el ID del préstamo, su campo `creditpolicy`, el monto del préstamo y el valor total de la cartera, como` eligible_collateral`.

El programa debe tomar dos parámetros de línea de comando, el nombre de archivo del archivo de salida de la parte 1 y el nombre del archivo de datos del préstamo, que se pueden ubicar localmente.

Datos de préstamo JSON: https://github.com/mlennard-utn/tp_avanzado/blob/master/prestamos.json

Por ejemplo, la primera cuenta que figura en el archivo (`loan1`) tiene 10 posiciones con un valor total, de acuerdo con los datos de precios de la parte 1, de $ 18,006,225.05. El monto pendiente de su préstamo es de $ 533,492 por lo que este préstamo está totalmente garantizado y no debe figurar en el archivo de salida.

Ejemplo de ejecución del programa (tenga en cuenta que los números son para fines ilustrativos, no provienen de los datos anteriores):
`` `
$ ./myprogram2 marketdata.json loandata.json

[
  {
    "id": "loan1234",
    "creditpolicy": "policy1234",
    "quantity": 10000,
    "eligible_collateral": 9999,
  },
...
]
`` `

---
---

## Link util con tutorial de Jackson Mapper:

http://tutorials.jenkov.com/java-json/jackson-objectmapper.html


---
---

# Entregable:

## Una vez descargado el codigo fuente (luego de hacer el checkout del repositorio que me indican) se debe ejecutar el siguiente comando: 
'''mvn clean compile assembly:single''' (o botón derecho sobre el projecto -> Run as -> Maven build... -> en la sección goals colocar clean compile assembly:single)

El resultado de la ejecucion del programa debería ser un archivo con extensión .jar en la carpeta "target" (sin hay algún error se debe revisar el contenido del tag <mainClass> colocando el paquete y nombre de la clase que posee el metodo main para la ejecucion del programa)

## La ejecución de la primera parte del ejercicio debería ser ejecutando el siguiente comando:
'''cd target''' (o posicionarse donde el archivo jar haya sido generado)
'''java -jar market.data-0.0.1-jar-with-dependencies.jar https://raw.githubusercontent.com/mlennard-utn/tp_avanzado/master/mercado.json'''
(en este caso el jar de ejemplo que se usa es market.data-0.0.1-jar-with-dependencies.jar)

Como resultado de la ejecución se mostrará en la pantalla el json solicitado y se generará un archivo con cierto nombre (por ejemplo marketdata.json) en el mismo directorio donde se está ejecutando.

## La segunda parte del ejercicio se debe probar ejecutando el siguiente comando:
'''java -jar market.data-0.0.1-jar-with-dependencies.jar marketdata.json loandata.json'''

