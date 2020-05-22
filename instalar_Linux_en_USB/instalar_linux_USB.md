# Tutorial para instalar Linux sobre un USB
Esto nos permitirá tener una instalación del SO Linux sobre un USB, y podremos usarlo cómo si fuera nuestro pc.  
- Permitirá guardar cambios, hacer instalaciones,... Igual que si estuvieramos trabajando sobre el Disco Duro del ordenador.
- En cualquier ordenador podremos tener nuestra configuración (la que esté almacenada en el USB)

Para hacer esto necesitaremos:
- Un [USB Booteable](../usb_booteable/crear_USB_booteable.md) con la distribución de Linux que queramos instalar.
- Un USB vacío, dónde haremos la instalación. (Recomendado min. 32Gb)

## Iniciamos la instalación
- Iniciamos el PC sobre el USB Booteable, quizás sea necesario [cambiar la configuración de la BIOS](../bios/ordenDeArranque.md).
- En el menú de inicio al arrancar, elegimos **Instalar**

- Seleccionamos el idioma de la instalación
    - Continuar

![Seleccionamos el idioma](img/3.2.png)

- Seleccionamos el idioma del teclado
    - Continuar

![Seleccionamos el idioma del teclado](img/3.3.png)


- Indicamos nuestra ubicación, para configurar la zona horaria
    - Continuar

![Indicar zona horaria](img/3.6.png)

- Configuramos la cuenta del usuario principal del equipo
    - Nombre
    - Nombre equipo
    - Nombre usuario
    - Contraseña
    - Solicitar contraseña para iniciar sesión (recomendado)
    - Continuar

![Configuración de usuario del sistema](img/3.7.png)



- Clicamos en descargar actualizaciones al finalizar instalación
- Clicamos para permitir instalar Software de terceros
    - Continuar  
La imagen no es correcta

![Click en permitir instalar software de terceros](img/3.4.png)

**OJO ESTA PARTE ES MUY IMPORTANTE**
- Aquí le indicamos a Linux que vamos a usar la partición que hemos creado.
- En este punto debemos elegir el tipo de instalación
    - Elegimos **Más Opciones**
    - Continuar

![Elegir tipo de instalación - Más opciones](img/3.5.0.png)

- Pulsamos sobre la línea que dice **espacio libre**
    - Doble click

![Doble click sobre espacio libre](img/3.5.1.png)

- Creamos la primera partición (dónde estarán los archivos de arranque de Linux)
    - Indicamos el tamaño (Recomendado aprox. 20Gb)
    - Utilizar como: *sistema de ficheros ext4 transacional*
    - Punto de montaje: */* (Esta es la carpeta raiz de Linux)
    - OK

![Creamos la primera partición](img/3.5.2.png)

- Aquí vemos que ya se ha creado la partición **/dev/sda5**
    - Vemos que ha cambiado el tamaño del espacio libre
    - Doble click sobre espacio libre

![Aquí ya se ve la primera partición](img/3.5.3.png)

- Creamos una partición para el intercambio
    - Indicamos el tamaño (Recomendado 1/2 de la RAM del equipo)
    - Utilizar como: *area de intercambio*
    - OK

![](img/3.5.4.2.png)
![](img/3.5.4.1.png)

- Vemos que ya está creada la partición de intercambio **/dev/sda6 swap**
- El espacio libre ha disminuido de nuevo
    - Doble click sobre espacio libre

![](img/3.5.5.1.png)

- Creamos la tercera partición, para los datos de los usuarios
    - Tamaño: dejamos el resto de espacio libre.
    - Utilizar como: *sistema de ficheros ext4 transacional*
    - Punto de montaje: **/home**
    - OK

![Creamos la tercera partición para los datos de los usuarios](img/3.5.5.2.png)

- Aquí ya vemos que se han creado las 3 particiones
- Ahora debemos configurar el **Dispositivo donde instalar el cargador de arranque**
    - Debemos elegir la partición para / que esté en el USB
    - En el caso de la imagen: **/dev/sda5**

![Vemos que se han creado las 3 particiones](img/3.5.6.png)

- Aquí ya vemos que se han creado las 3 particiones
- Y hemos elegido el dispositivo donde instalar el cargador de arranque.
- Ya podemos seguir con la instalación
    - Pulsamos en instalar ahora

![Vemos que se han creado las 3 particiones](img/3.5.6.png)

- Nos salta una ventana de confirmación, para que confirmemos que queremos formatear las nuevas particiones e instalar Linux en ellas.
    - Si todo es Ok, pulsamos **Continuar**

![Confirmamos que las particiones son correctas](img/3.5.7.png)


- Aquí empieza la instalación de todos los archivos del sistema

![Instalación del sistema](img/3.8.png)

- Reiniciamos el ordenador.
- Pulsamos la tecla para elegir unidad de arranque, en mi caso F9, y elegimos el USB.
- En el menú de inicio, ya no aparece instalar, elegimos la primera opción, e iniciamos Linux.
- Introducimos nuestro password

![Seleccionar SO para iniciar equipo](img/4.0.1.png)

**Ya tenemos nuestra instalación de Linux en un USB**

![Pantalla de escritorio en Linux](img/4.1.png)

- Una vez iniciado, se recomienda actualizar.

YA ESTÁ !!!


