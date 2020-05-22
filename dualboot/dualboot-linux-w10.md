# Tutorial para crear un dual boot con Windows 10 y Linux Mint

Para poder hacer esto necesitaremos:
- Tener un dvd de instalación de Linux o un [USB booteable](../usb_booteable/crear_USB_booteable.md) que contenga la imagen ISO de la distribución de Linux que queremos Instalar.
- [Modificar el arranque de la BIOS](../bios/ordenDeArranque.md), para que arranque desde el USB.

---

1. Vamos a crear una partición en nuestro disco duro, para poder instalar Linux en esta.  
    - Click con el botón derecho sobre **Este equipo**
    - Click sobre administrar  

![Hacer click derecho sobre este equipo](./img/2.1.PNG)
- Ahora debemos pulsar sobre **Administración de discos** 

![Pulsamos en administración de discos](./img/2.2.PNG)

- Luego pulsamos sobre el disco que queremos reducir  
    - Botón derecho
    - Reducir volumen 

![Botón derecho sobre el disco a reducir](./img/2.3.PNG)

- Le indicamos el tamaño en MB que queremos que se reduzca la partición
    - Reducir

![Indicar la cantidad en MB que queremos reducir](./img/2.4.PNG)

- Ahora ya tenemos una partición, del tamaño indicado, que no está asignada.
    - Esta es la partición que usaremos para instalar Linux

![Ya tenemos la partición, no asignada](./img/2.5.PNG)

- Ahora reiniciamos Windows
    - **Recuerda insertar el USB Booteable, antes del reinicio**

![Reiniciamos Windows](./img/2.6.PNG)

Aquí me falta la imagen de cuando el USB Booteable carga, solicitando elegir boot

- Iniciamos Linux desde el USB
    - Pulsamos sobre el disco, para instalar Linux Mint

![Iniciamos linux desde el USB](./img/3.1.PNG)

## Esto inicia el proceso de instalación
- Seleccionamos el idioma de la instalación
    - Continuar

![Seleccionamos el idioma](./img/3.2.PNG)

- Seleccionamos el idioma del teclado
    - Continuar

![Seleccionamos el idioma del teclado](./img/3.3.PNG)

- Clicamos para permitir instalar Software de terceros
    - Continuar

![Click en permitir instalar software de terceros](./img/3.4.PNG)

**OJO ESTA PARTE ES MUY IMPORTANTE**
- Aquí le indicamos a Linux que vamos a usar la partición que hemos creado.
- En este punto debemos elegir el tipo de instalación
    - Elegimos **Más Opciones**
    - Continuar

![Elegir tipo de instalación - Más opciones](./img/3.5.0.PNG)

- Pulsamos sobre la línea que dice **espacio libre**
    - Doble click

![Doble click sobre espacio libre](./img/3.5.1.PNG)

- Creamos la primera partición (dónde estarán los archivos de arranque de Linux)
    - Indicamos el tamaño (Recomendado aprox. 20Gb)
    - Utilizar como: *sistema de ficheros ext4 transacional*
    - Punto de montaje: */* (Esta es la carpeta raiz de Linux)
    - OK

![Creamos la primera partición](./img/3.5.2.PNG)

- Aquí vemos que ya se ha creado la partición **/dev/sda5**
    - Vemos que ha cambiado el tamaño del espacio libre
    - Doble click sobre espacio libre

![Aquí ya se ve la primera partición](./img/3.5.3.PNG)

- Creamos una partición para el intercambio
    - Indicamos el tamaño (Recomendado 1/2 de la RAM del equipo)
    - Utilizar como: *área de intercambio*
    - OK

![Seleccionar utilizar como área de intercambio](./img/3.5.4.2.PNG)
![Creamos una partición para el intercambio](./img/3.5.4.1.PNG)

- Vemos que ya está creada la partición de intercambio **/dev/sda6 swap**
- El espacio libre ha disminuido de nuevo
    - Doble click sobre espacio libre

![Vemos que se ha creado la partición de intercambio SWAP](./img/3.5.5.1.PNG)

- Creamos la tercera partición, para los datos de los usuarios
    - Tamaño: dejamos el resto de espacio libre.
    - Utilizar como: *sistema de ficheros ext4 transacional*
    - Punto de montaje: **/home**
    - OK

![Creamos la tercera partición para los datos de los usuarios](./img/3.5.5.2.PNG)

- Aquí ya vemos que se han creado las 3 particiones
- Ya podemos seguir con la instalación
    - Pulsamos en instalar ahora

![Vemos que se han creado las 3 particiones](./img/3.5.6.PNG)

- Nos salta una ventana de confirmación, para que confirmemos que queremos formatear las nuevas particiones e instalar Linux en ellas.
    - Si todo es Ok, pulsamos **Continuar**

![Confirmamos que las particiones son correctas](./img/3.5.7.PNG)

- Indicamos nuestra ubicación, para configurar la zona horaria
    - Continuar

![Indicar zona horaria](./img/3.6.PNG)

- Configuramos la cuenta del usuario principal del equipo
    - Nombre
    - Nombre equipo
    - Nombre usuario
    - Contraseña
    - Solicitar contraseña para iniciar sesión (recomendado)
    - Continuar

![Configuración de usuario del sistema](./img/3.7.PNG)

- Aquí empieza la instalación de todos los archivos del sistema

![Instalación del sistema](./img/3.8.PNG)

- Al finalizar la instalación, ya podemos reiniciar el sistema.
    - Reiniciar ahora

![Fin de instalación - Reiniciar ahora](./img/3.9.PNG)

- Al reiniciar el equipo tenemos la opción de elegir que SO queremos iniciar

![Seleccionar SO para iniciar equipo](./img/4.0.PNG)

- Introducimos nuestro password

![Seleccionar SO para iniciar equipo](./img/4.0.1.PNG)

**Ya tenemos nuestra instalación de Linux en Windows 10**

![Pantalla de escritorio en Linux](./img/4.1.PNG)


