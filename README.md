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





###### Préstamos

| ID Préstamo | ID Cliente | Monto del préstamo | Tasa de interés | Fecha de desembolso | Fecha de vencimiento | Saldo pendiente | Estado del préstamo |
|:-----------:|:----------:|:------------------:|:---------------:|:-------------------:|:--------------------:|:---------------:|:---------------------:|
|1|495798|964203.64|6.63|2023-11-19|2032-06-06|674174.18|Vencido|
|2|42734|811935.67|13.42|2023-05-07|2028-08-29|756664.53|Activo|
|3|540710|961457.89|13.68|2021-10-28|2030-03-10|200162.19|Vencido|
|4|983331|78869.24|11.42|2023-05-14|2026-12-17|67546.61|Vencido|
|5|409214|456168.05|6.93|2020-05-18|2026-07-08|729762.37|Activo|

##### 1FN
Los datos cumplen con la Primera Forma Normal.

##### 2FN
Estado del préstamo presenta redundancia de datos, por lo que se creará otra entidad para eliminar la duplicidad de datos.

###### Préstamos

| ID Préstamo | ID Cliente | Monto del préstamo | Tasa de interés | Fecha de desembolso | Fecha de vencimiento | Saldo pendiente | ID Estado del préstamo |
|:-----------:|:----------:|:------------------:|:---------------:|:-------------------:|:--------------------:|:---------------:|:------------------------:|
|1|495798|964203.64|6.63|2023-11-19|2032-06-06|674174.18|1|
|2|42734|811935.67|13.42|2023-05-07|2028-08-29|756664.53|2|
|3|540710|961457.89|13.68|2021-10-28|2030-03-10|200162.19|1|
|4|983331|78869.24|11.42|2023-05-14|2026-12-17|67546.61|1|
|5|409214|456168.05|6.93|2020-05-18|2026-07-08|729762.37|2|

###### Estado del préstamo

| ID | Estado préstamo |
|:--:|:---------------:|
|1|Vencido|
|2|Activo|
|...|...|

##### 3FN
Los datos cumplen con la Tercera Formal Normal.





###### Tarjetas crédito

| ID Tarjeta | ID Cliente | Número de tarjeta | Límite de crédito | Saldo actual | Fecha de emisión | Fecha de expiración | Estado | Fecha de corte | Día del ciclo |
|:----------:|:----------:|:-----------------:|:-----------------:|:------------:|:----------------:|:-------------------:|:------:|:--------------:|:-------------:|
|1|558120|4872410269895827|4344.96|20358.67|2022-02-09|2025-05-04|Bloqueada|2022-03-06|6|
|2|443984|4780431200473540|48263.8|12583.92|2021-04-29|2025-11-10|Activa|2021-05-26|26|
|3|709855|4653562424107275|37894.69|16274.3|2021-12-10|2026-08-08|Bloqueada|2022-01-08|8|
|4|495584|4935123661880312|3610.3|31113.15|2020-11-21|2025-07-26|Bloqueada|2020-12-18|18|
|5|621646|4918591621061050|35118.01|5054.92|2023-10-06|2028-02-05|Cancelada|2023-11-05|5|

##### 1FN
Los datos cumplen con la Primera Forma Normal.

##### 2FN
Estado presenta redundancia de datos, por lo que se creará otra entidad para eliminar la duplicidad de datos.

###### Tarjetas crédito

| ID Tarjeta | ID Cliente | Número de tarjeta | Límite de crédito | Saldo actual | Fecha de emisión | Fecha de expiración | ID Estado | Fecha de corte | Día del ciclo |
|:----------:|:----------:|:-----------------:|:-----------------:|:------------:|:----------------:|:-------------------:|:---------:|:--------------:|:-------------:|
|1|558120|4872410269895827|4344.96|20358.67|2022-02-09|2025-05-04|2|2022-03-06|6|
|2|443984|4780431200473540|48263.8|12583.92|2021-04-29|2025-11-10|1|2021-05-26|26|
|3|709855|4653562424107275|37894.69|16274.3|2021-12-10|2026-08-08|2|2022-01-08|8|
|4|495584|4935123661880312|3610.3|31113.15|2020-11-21|2025-07-26|2|2020-12-18|18|
|5|621646|4918591621061050|35118.01|5054.92|2023-10-06|2028-02-05|3|2023-11-05|5|

###### Estado del préstamo

| ID | Estado |
|:--:|:------:|
|1|Activo|
|2|Bloqueado|
|3|Cancelada|
|...|...|

##### 3FN
Los datos cumplen con la Tercera Formal Normal.





###### Sucursal/Agencia

| ID | Nombre | Tipo | Departamento | Municipio | Dirección | Código postal | Teléfono |
|:--:|:------:|:----:|:------------:|:---------:|:---------:|:-------------:|:--------:|
|1|Sucursal Antigua Guatemala 1|Sucursal|Sacatepéquez|Antigua Guatemala|Zona 7|91405|+502 8036-8423|
|2|Sucursal Escuintla 2|Sucursal|Escuintla|Escuintla|Zona 1|97145|+502 9525-7114|
|3|Sucursal Quetzaltenango 3|Sucursal|Quetzaltenango|Quetzaltenango|Zona 1|53915|+502 2873-4763|
|4|Sucursal Cobán 4|Sucursal|Alta Verapaz|Cobán|Zona 8|31535|+502 6809-5562|
|5|Sucursal Flores 5|Sucursal|Petén|Flores|Zona 10|63389|+502 5942-1959|

Se modificará el nombre de la entidad a Punto servicio para que sea más general.

##### 1FN
Los datos cumplen con la Primera Forma Normal.

##### 2FN
Tipo, Departamento, Municipio y Código postal presentan redundancia de datos, por lo que se creará otra entidad para eliminar la duplicidad de datos. No tomaré en cuenta dirección, en caso de que se ingrese una dirección con calles, avenidas y demás información.

###### Puntos servicio

| ID | Nombre | ID Tipo | ID Departamento | ID Municipio | Dirección | ID Código postal | Teléfono |
|:--:|:------:|:-------:|:---------------:|:------------:|:---------:|:----------------:|:--------:|
|1|Sucursal Antigua Guatemala 1|1|1|1|Zona 7|1|+502 8036-8423|
|2|Sucursal Escuintla 2|1|2|2|Zona 1|2|+502 9525-7114|
|3|Sucursal Quetzaltenango 3|1|3|3|Zona 1|3|+502 2873-4763|
|4|Sucursal Cobán 4|1|4|4|Zona 8|4|+502 6809-5562|
|5|Sucursal Flores 5|1|5|5|Zona 10|5|+502 5942-1959|

###### Tipo

| ID | Tipo |
|:--:|:----:|
|1|Sucursal|
|2|Agencia|

###### Departamento

| ID | Departamento |
|:--:|:------------:|
|1|Sacatepéquez|
|2|Escuintla|
|3|Quetzaltenango|
|4|Alta Verapaz|
|5|Petén|
|...|...|

###### Municipio

| ID | Municipio |
|:--:|:---------:|
|1|Antigua Guatemala|
|2|Escuintla|
|3|Quetzaltenango|
|4|Cobán|
|5|Flores|
|...|...|

###### Código postal

| ID | Código postal |
|:--:|:-------------:|
|1|91405|
|2|97145|
|3|53915|
|4|31535|
|5|63389|
|...|...|

##### 3FN
Los datos cumplen con la Tercera Formal Normal.
En este caso, ID Departamento, ID Municipio, Dirección y ID Código postal dependen entre sí para formar una ubicación, por lo que se creará otra entidad para contener dichos valores.

###### Puntos servicio

| ID | Nombre | ID Tipo | ID Departamento | ID Municipio | Dirección | ID Código postal | Teléfono |
|:--:|:------:|:-------:|:---------------:|:------------:|:---------:|:----------------:|:--------:|
|1|Sucursal Antigua Guatemala 1|1|1|1|Zona 7|1|+502 8036-8423|
|2|Sucursal Escuintla 2|1|2|2|Zona 1|2|+502 9525-7114|
|3|Sucursal Quetzaltenango 3|1|3|3|Zona 1|3|+502 2873-4763|
|4|Sucursal Cobán 4|1|4|4|Zona 8|4|+502 6809-5562|
|5|Sucursal Flores 5|1|5|5|Zona 10|5|+502 5942-1959|

###### Tipo

| ID | Tipo |
|:--:|:----:|
|1|Sucursal|
|2|Agencia|

###### Ubicación

| ID | ID Departamento | ID Municipio | Dirección | Código postal |
|:--:|:---------------:|:------------:|:---------:|:-------------:|
|1|1|1|Zona 7|1|
|2|2|2|Zona 1|2|
|3|3|3|Zona 1|3|
|4|4|4|Zona 8|4|
|5|5|5|Zona 10|5|
|...|...|...|...|...|

###### Departamento

| ID | Departamento |
|:--:|:------------:|
|1|Sacatepéquez|
|2|Escuintla|
|3|Quetzaltenango|
|4|Alta Verapaz|
|5|Petén|
|...|...|

###### Municipio

| ID | Municipio |
|:--:|:---------:|
|1|Antigua Guatemala|
|2|Escuintla|
|3|Quetzaltenango|
|4|Cobán|
|5|Flores|
|...|...|

###### Código postal

| ID | Código postal |
|:--:|:-------------:|
|1|91405|
|2|97145|
|3|53915|
|4|31535|
|5|63389|
|...|...|





###### Empleados

| ID | Nombre | Apellido | Rol | Departamento | Sucursal/Asignación | Teléfono |
|:--:|:------:|:--------:|:---:|:------------:|:-------------------:|:--------:|
|1|Nombre_1|Apellido_1|Auditor Interno|Petén|Sucursal/Agencia 528|+502 7815-2167|
|2|Nombre_2|Apellido_2|Administrador|Chiquimula|Sucursal/Agencia 171|+502 3808-9764|
|3|Nombre_3|Apellido_3|Atención al Cliente|Jutiapa|Sucursal/Agencia 103|+502 4899-1699|
|4|Nombre_4|Apellido_4|Oficial de Crédito|Quetzaltenango|Sucursal/Agencia 36|+502 3452-1726|
|5|Nombre_5|Apellido_5|Soporte Técnico|Jutiapa|Sucursal/Agencia 583|+502 8283-6524|

##### 1FN
La columna sucursal/asignación no cumple con la Primera Forma Normal. En este caso, se debe asociar a la tabla de Puntos servicio por medio del ID de la misma

| ID | Nombre | Apellido | Rol | Departamento | ID Punto venta | Teléfono |
|:--:|:------:|:--------:|:---:|:------------:|:--------------:|:--------:|
|1|Nombre_1|Apellido_1|Auditor Interno|Petén|528|+502 7815-2167|
|2|Nombre_2|Apellido_2|Administrador|Chiquimula|171|+502 3808-9764|
|3|Nombre_3|Apellido_3|Atención al Cliente|Jutiapa|103|+502 4899-1699|
|4|Nombre_4|Apellido_4|Oficial de Crédito|Quetzaltenango|36|+502 3452-1726|
|5|Nombre_5|Apellido_5|Soporte Técnico|Jutiapa|583|+502 8283-6524|

##### 2FN
Rol y Departamento presentan redundancia de datos, por lo que se creará otra entidad para eliminar la duplicidad de datos. En el caso de Departamento, esta columna se quitará, ya que la sucursal indica la ubicación y con ello el departamento.

| ID | Nombre | Apellido | ID Rol | ID Punto venta | Teléfono |
|:--:|:------:|:--------:|:------:|:--------------:|:--------:|
|1|Nombre_1|Apellido_1|1|528|+502 7815-2167|
|2|Nombre_2|Apellido_2|2|171|+502 3808-9764|
|3|Nombre_3|Apellido_3|3|103|+502 4899-1699|
|4|Nombre_4|Apellido_4|4|36|+502 3452-1726|
|5|Nombre_5|Apellido_5|5|583|+502 8283-6524|

###### Rol

| ID | Rol |
|:--:|:---:|
|1|Auditor Interno|
|2|Administrador|
|3|Atención al Cliente|
|4|Oficial de Crédito|
|5|Soporte Técnico|
|...|...|

##### 3FN
Los datos cumplen con la Tercera Formal Normal.

### ENTIDADES
Luego de llevar a cabo el proceso de normalización, se obtuvieron las siguiente entidades:

* Cliente
* Cuenta
* Tipo cuenta
* Transacción
* Tipo transacción
* Préstamo
* Estado préstamo
* Tarjeta crédito
* Estado tarjeta
* Punto servicio
* Tipo
* Departamento
* Municipio
* Código postal
* Ubicación
* Empleado
* Rol

### DIAGRAMA MATRICIAL

| ENTIDADES | Cliente | Cuenta | Tipo cuenta | Transacción | Tipo transacción | Préstamo | Estado préstamo | Tarjeta crédito | Estado tarjeta | Punto servicio | Tipo | Departamento | Municipio | Código postal | Ubicación | Empleado | Rol |
|:---------:|:-------:|:------:|:-----------:|:-----------:|:----------------:|:--------:|:---------------:|:---------------:|:--------------:|:--------------:|:----:|:------------:|:---------:|:-------------:|:---------:|:--------:|:---:|
|Cliente|-|tener|-|realizar|-|realizar|-|tener|-|-|-|-|-|-|-|-|-|
|Cuenta|pertenecer a|-|tener|estar asociada a|-|-|-|-|-|-|-|-|-|-|-|-|-|
|Tipo cuenta|-|clasificar|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
|Transacción|ser realizada por|contener|-|-|tener|-|-|-|-|generarse en|-|-|-|-|-|-|-|
|Tipo transacción|-|-|-|clasificar|-|-|-|-|-|-|-|-|-|-|-|-|-|
|Préstamo|ser realizado por|-|-|-|-|-|tener|-|-|-|-|-|-|-|-|-|-|
|Estado préstamo|-|-|-|-|-|clasificar|-|-|-|-|-|-|-|-|-|-|-|
|Tarjeta crédito|pertenecer a|-|-|-|-|-|-|-|tener|-|-|-|-|-|-|-|-|
|Estado tarjeta|-|-|-|-|-|-|-|clasificar|-|-|-|-|-|-|-|-|-|
|Punto servicio|-|-|-|generar|-|-|-|-|-|-|tener|-|-|-|tener|contener|-|
|Tipo|-|-|-|-|-|-|-|-|-|clasificar|-|-|-|-|-|-|-|
|Departamento|-|-|-|-|-|-|-|-|-|-|-|-|-|-|pertencer a|-|-|
|Municipio|-|-|-|-|-|-|-|-|-|-|-|-|-|-|pertencer a|-|-|
|Código postal|-|-|-|-|-|-|-|-|-|-|-|-|-|-|pertencer a|-|-|
|Ubicación|-|-|-|-|-|-|-|-|-|pertenecer a|-|tener|tener|tener|-|-|-|
|Empleado|-|-|-|-|-|-|-|-|-|trabajar en|-|-|-|-|-|-|asumir|
|Rol|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|ser asumido por|-|