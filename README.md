De acuerdo a los datos proporcionados y disponibles en los archivos con extensión .csv, se pueden identificar las siguientes entidades y atributos:

#### 1. Clientes
* ID
* Nombre
* Apellido
* Número de cuenta
* Tipo de cuenta
* Saldo
* Teléfono

#### 2. Transacciones
* ID Transacción
* ID Cliente
* Número de cuenta
* Tipo de transacción
* Monto
* Fecha
* Hora
* Descripción
* Sucursal/Agencia

#### 3. Préstamos
* ID Préstamo
* ID Cliente
* Monto del préstamo
* Tasa de interés
* Fecha de desembolso
* Fecha de vencimiento
* Saldo pendiente
* Estado del préstamo

#### 4. Tarjetas de crédito
* ID Tarjeta
* ID Cliente
* Número de tarjeta
* Límite de crédito
* Saldo actual
* Fecha de emisión
* Fecha de expiración
* Estado
* Fecha de corte
* Día del ciclo

#### 5. Sucursales/Agencias
* ID
* Nombre
* Tipo
* Departamento
* Municipio
* Dirección
* Código postal
* Teléfono

#### 6. Empleados
* ID
* Nombre
* Apellido
* Rol
* Departamento
* Sucursal/Asignación
* Teléfono

Sin embargo, estos datos no se manejarán exactamente como fueron dados, sino que es necesario que se lleve a cabo el proceso de normalización. La normalización consiste en aplicar una serie de reglas a los datos con el objetivo de minimizar la redundancia. Este proceso es esencial para organizar y estructurar correctamente los datos, asimismo para mejorar la integridad y consistencia de los mismos.

En este proyecto se aplicaron las primeras tres formas de normalización, las cuales se describen a continuación:

#### 1FN
La Primera Forma Normal consiste en verificar que los atributos sean atómicos, es decir, simples e indivisibles.

#### 2FN
La Segunda Forma Normal en primer lugar debe cumplir con la forma 1FN. Luego examina que todos aquellos atributos que no son o forman parte de la clave primaria dependan completamente de esta.

#### 3FN
La Tercera Forma Normal debe cumplir con la forma 2FN. Después verifica que los atributos no clave no dependan de otro atributo no clave.

Una vez descrito el proceso de normalización y las tres formas normales a utilizar, se llevará a cabo dicho proceso con las entidades y atributos listados anteriormente.


#### Clientes

| ID | Nombre | Apellido | Número de cuenta | Tipo de cuenta | Saldo | Teléfono |
|:--:|:------:|:--------:|:----------------:|:--------------:|:-----:|:--------:|
|1|Nombre_1|Apellido_1|70186741-1|Ahorro|256848.49|+502 4634-7041|
|2|Nombre_2|Apellido_2|42148275-2|Ahorro|378588.21|+502 2701-1140|
|3|Nombre_3|Apellido_3|95968205-3|Depósito Monetario|294799.84|+502 6277-2079|
|4|Nombre_4|Apellido_4|74601803-4|Ahorro|30357.74|+502 7371-9552|
|5|Nombre_5|Apellido_5|18184518-5|Ahorro|270027.6|+502 1699-8122|

Se consideró agregar dos campos más, uno para almacenar la fecha de creación del cliente y otro para la fecha de modificación del mismo. Con ello, la tabla quedaría de esta forma:

| ID | Nombre | Apellido | Número de cuenta | Tipo de cuenta | Saldo | Teléfono | Creation date | Modification date |
|:--:|:------:|:--------:|:----------------:|:--------------:|:-----:|:--------:|:-------------:|:-----------------:|
|1|Nombre_1|Apellido_1|70186741-1|Ahorro|256848.49|+502 4634-7041|dd-MM-yyyy HH:mm:ss|dd-MM-yyyy HH:mm:ss|
|2|Nombre_2|Apellido_2|42148275-2|Ahorro|378588.21|+502 2701-1140|dd-MM-yyyy HH:mm:ss|dd-MM-yyyy HH:mm:ss|
|3|Nombre_3|Apellido_3|95968205-3|Depósito Monetario|294799.84|+502 6277-2079|dd-MM-yyyy HH:mm:ss|dd-MM-yyyy HH:mm:ss|
|4|Nombre_4|Apellido_4|74601803-4|Ahorro|30357.74|+502 7371-9552|dd-MM-yyyy HH:mm:ss|dd-MM-yyyy HH:mm:ss|
|5|Nombre_5|Apellido_5|18184518-5|Ahorro|270027.6|+502 1699-8122|dd-MM-yyyy HH:mm:ss|dd-MM-yyyy HH:mm:ss|

Una vez agregados los campos, se aplicarán las reglas de normalización.

##### 1FN
Los datos cumplen con la Primera Forma Normal.

##### 2FN
En este caso, el tipo de cuenta presenta redundancia, por lo que se creará otra entidad para ello.

###### Clientes

| ID | Nombre | Apellido | Número de cuenta | ID Tipo de cuenta | Saldo | Teléfono | Creation date | Modification date |
|:--:|:------:|:--------:|:----------------:|:-----------------:|:-----:|:--------:|:-------------:|:-----------------:|
|1|Nombre_1|Apellido_1|70186741-1|1|256848.49|+502 4634-7041|dd-MM-yyyy HH:mm:ss|dd-MM-yyyy HH:mm:ss|
|2|Nombre_2|Apellido_2|42148275-2|1|378588.21|+502 2701-1140|dd-MM-yyyy HH:mm:ss|dd-MM-yyyy HH:mm:ss|
|3|Nombre_3|Apellido_3|95968205-3|2|294799.84|+502 6277-2079|dd-MM-yyyy HH:mm:ss|dd-MM-yyyy HH:mm:ss|
|4|Nombre_4|Apellido_4|74601803-4|1|30357.74|+502 7371-9552|dd-MM-yyyy HH:mm:ss|dd-MM-yyyy HH:mm:ss|
|5|Nombre_5|Apellido_5|18184518-5|1|270027.6|+502 1699-8122|dd-MM-yyyy HH:mm:ss|dd-MM-yyyy HH:mm:ss|

###### Tipo de cuenta

| ID | Tipo de cuenta |
|:--:|:--------------:|
|1|Ahorro|
|2|Depósito Monetario|
|...|...|

##### 3FN
Los atributos que no son clave no pueden depender de otros atributos distintos a la clave. En la tabla Número de cuenta, ID Tipo de cuenta, Saldo dependen entre sí. Por tanto, se creará una nueva entidad para los datos de las cuentas.

###### Clientes

| ID | Nombre | Apellido | Teléfono | Creation date | Modification date |
|:--:|:------:|:--------:|:--------:|:-------------:|:-----------------:|
|1|Nombre_1|Apellido_1|+502 4634-7041|dd-MM-yyyy HH:mm:ss|dd-MM-yyyy HH:mm:ss|
|2|Nombre_2|Apellido_2|+502 2701-1140|dd-MM-yyyy HH:mm:ss|dd-MM-yyyy HH:mm:ss|
|3|Nombre_3|Apellido_3|+502 6277-2079|dd-MM-yyyy HH:mm:ss|dd-MM-yyyy HH:mm:ss|
|4|Nombre_4|Apellido_4|+502 7371-9552|dd-MM-yyyy HH:mm:ss|dd-MM-yyyy HH:mm:ss|
|5|Nombre_5|Apellido_5|+502 1699-8122|dd-MM-yyyy HH:mm:ss|dd-MM-yyyy HH:mm:ss|

###### Cuentas

| ID | Número de cuenta | ID Tipo de cuente | ID Cliente | Saldo |
|:--:|:----------------:|:-----------------:|:----------:|:-----:|
|1|70186741-1|1|1|256848.49|
|2|42148275-2|1|2|378588.21|
|3|95968205-3|2|3|294799.84|
|4|74601803-4|1|4|30357.74|
|5|18184518-5|1|5|270027.6|

###### Tipo de cuenta

| ID | Tipo de cuenta |
|:--:|:--------------:|
|1|Ahorro|
|2|Depósito Monetario|
|...|...|


#### Transacciones

| ID Transacción | ID Cliente | Número de cuenta | Tipo de transacción | Monto | Fecha | Hora | Descripción | Sucursal/Agencia |
|:--------------:|:----------:|:----------------:|:-------------------:|:-----:|:-----:|:----:|:-----------:|:----------------:|
|1|455902|58639163-455902|Transferencia|2865.8|2023-10-24|14:28:01|Transacción de tipo Transferencia|Sucursal/Agencia 221|
|2|469824|99757988-469824|Depósito|2438.92|2023-12-09|14:28:01|Transacción de tipo Depósito|Sucursal/Agencia 257|
|3|626567|19969005-626567|Transferencia|9494.98|20204-06-01|14:28:01|Transacción de tipo Transferencia|Sucursal/Agencia 874|
|4|784443|95861936-784443|Pago|8399.08|2023-12-26|14:28:01|Transacción de tipo Pago|Sucursal/Agencia 265|
|5|421423|21672609-421423|Depósito|7722.1|2022-12-27|14:28:01|Transacción de tipo Depósito|Sucursal/Agencia 986|

Se consideró manejar la fecha y hora en una sola columna. La tabla quedaría de la siguiente forma:

| ID Transacción | ID Cliente | Número de cuenta | Tipo de transacción | Monto | Fecha | Descripción | Sucursal/Agencia |
|:--------------:|:----------:|:----------------:|:-------------------:|:-----:|:-----:|:-----------:|:----------------:|
|1|455902|58639163-455902|Transferencia|2865.8|2023-10-24 14:28:01|Transacción de tipo Transferencia|Sucursal/Agencia 221|
|2|469824|99757988-469824|Depósito|2438.92|2023-12-09 14:28:01|Transacción de tipo Depósito|Sucursal/Agencia 257|
|3|626567|19969005-626567|Transferencia|9494.98|20204-06-01 14:28:01|Transacción de tipo Transferencia|Sucursal/Agencia 874|
|4|784443|95861936-784443|Pago|8399.08|2023-12-26 14:28:01|Transacción de tipo Pago|Sucursal/Agencia 265|
|5|421423|21672609-421423|Depósito|7722.1|2022-12-27 14:28:01|Transacción de tipo Depósito|Sucursal/Agencia 986|

Una vez realizado este cambio, se realizará el proceso de normalización.

##### 1FN
* La columna de Número de cuenta no cumple con la Primera Forma Normal, ya que se tienen los ID de dos cuentas en una sola columna, por lo que se debe separar en Cuenta de origen y Cuenta destino.
* La columna Sucursal/Asignación no cumple con la Primera Forma Normal. En este caso, se debe asociar con el ID de la tabla Sucursales/Agencias (la cual cambiará de nombre a Punto venta).

##### Transacciones

|ID Transacción|ID Cliente|Número de cuenta origen|Número de cuenta destino|Tipo de transacción|Monto|Fecha|Descripción|ID Punto de venta|
|:------------:|:--------:|:---------------------:|:----------------------:|:-----------------:|:---:|:---:|:---------:|:---------------:|
|1|455902|58639163|455902|Transferencia|2865.8|2023-10-24 14:28:01|Transacción de tipo Transferencia|221|
|2|469824|99757988|469824|Depósito|2438.92|2023-12-09 14:28:01|Transacción de tipo Depósito|257|
|3|626567|19969005|626567|Transferencia|9494.98|20204-06-01 14:28:01|Transacción de tipo Transferencia|874|
|4|784443|95861936|784443|Pago|8399.08|2023-12-26 14:28:01|Transacción de tipo Pago|265|
|5|421423|21672609|421423|Depósito|7722.1|2022-12-27 14:28:01|Transacción de tipo Depósito|986|

##### 2FN
Tipo de transacción presenta redundancia de datos, por lo que se creará otra entidad para eliminar la duplicidad de datos.

##### Transacciones

|ID Transacción|ID Cliente|Número de cuenta origen|Número de cuenta destino|ID Tipo de transacción|Monto|Fecha|Descripción|ID Punto de venta|
|:------------:|:--------:|:---------------------:|:----------------------:|:--------------------:|:---:|:---:|:---------:|:---------------:|
|1|455902|58639163|455902|1|2865.8|2023-10-24 14:28:01|Transacción de tipo Transferencia|221|
|2|469824|99757988|469824|2|2438.92|2023-12-09 14:28:01|Transacción de tipo Depósito|257|
|3|626567|19969005|626567|1|9494.98|20204-06-01 14:28:01|Transacción de tipo Transferencia|874|
|4|784443|95861936|784443|3|8399.08|2023-12-26 14:28:01|Transacción de tipo Pago|265|
|5|421423|21672609|421423|2|7722.1|2022-12-27 14:28:01|Transacción de tipo Depósito|986|

###### Tipo de transacción

| ID | Tipo de transacción |
|:--:|:-------------------:|
|1|Transferencia|
|2|Depósito|
|3|Pago|
|...|...|

##### 3FN
Los datos cumplen con la Tercera Formal Normal.
