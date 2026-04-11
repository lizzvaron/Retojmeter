# Instrucciones paso a paso para ejecutar la prueba de carga del servicio de login

## Tecnologías y versiones recomendadas
- Apache JMeter 5.6.3
- Java JDK 17 (requerido por JMeter)
- Sistema operativo: Windows 10/11 o Linux (Ubuntu 20.04+)
- Editor de texto para preparar el archivo CSV (Excel)

## Pasos de ejecución

1. **Instalar JMeter**
   - Descargar Apache JMeter desde https://jmeter.apache.org
   - Descomprimir el paquete y verificar que Java esté instalado con `java -version`.

2. *Preparar archivo CSV*
   - Crear un archivo llamado `Usuarios.csv` con el siguiente contenido:
     
     user,passwd
     donero,ewedon
     kevinryan,kev02937@
     johnd,m38rmF$
     derek,jlkg*_56
     mor_2314,83r5^_
     
   - Guardar en la carpeta de pruebas de JMeter.

3. *Configurar prueba en JMeter*
   - Abrir JMeter y crear un Thread Group con al menos 20 hilos para simular 20 TPS.
   - Añadir un CSV Data Set Config apuntando al archivo `Usuarios.csv`.
   - Añadir un HTTP Request Sampler:
     - Método: POST
     - URL: `https://fakestoreapi.com/auth/login`
     - Body Data: `{"username":"${user}","password":"${passwd}"}`

4. *Añadir validaciones*
   - En el Response Assertion, validar que el código de respuesta sea `200`.
   - Configurar el Aggregate Report para medir:
     - Tiempo de respuesta ≤ 1500 ms
     - Tasa de error < 3%

5. *Ejecutar prueba*
   - Guardar el plan de prueba.
   - Ejecutar y observar métricas en el Aggregate Report y Summary Report.

6. *Interpretar resultados*
   - Confirmar que se alcanzan los 20 TPS.
   - Validar que el tiempo de respuesta promedio esté dentro del límite.
   - Revisar que la tasa de error sea menor al 3%.
