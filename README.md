# Bases de Datos de Grafos NeoJ
En este ejemplo se dará los primeros pasos con Neo4J.

## Creamos una cuenta en Digital Ocean.

1. Con el siguiente enlace usted recibirá 200 USD por 60 días: https://m.do.co/c/bf0ebb2acf6b
2. Cree la cuenta y configure una tarjeta de crédito o débito (con habilitación para compras por internet).
3. Recuerde que en Digital Ocean todo uso se cobra, las maquinas se cobran aún si estan apagadas.


## Creamos un par de llaves RSA para conectarnos al servidor.

### Windows 

Para Windows se necesitan dos herramientas que se ejecutan directamente:

1. Putty: Descarga el INSTALADOR de: https://the.earth.li/~sgtatham/putty/latest/w64/putty-64bit-0.78-installer.msi
2. Instalar

El instalador contiene dos herramientas Putty y PuttyGen.

Ahora se debe generar un par de llaves para esto siga las siguientes instrucciones: https://www.ibm.com/docs/es/spectrumvirtualizecl/8.5.x?topic=host-generating-ssh-key-pair-using-putty o puede ver este video https://youtu.be/Ahx7ElA9pIs?t=88

DEBE GUARDAR LA CADENA QUE SALE EN: `Public Key for pasting into OpenSSH authorizated_keys file`.

El contenido debería ser similar a:

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDZKI6cEHlIXDBUhWkHD/NtBp/kHN6jWELK+a2d1xpHf0ol+Zm5LLSnzFbQvgXzBFlZPPvB3bFmyq0QkU+Z7gSza6bYk5nQSf8NmF/ZaboQwR3sael9NnV7yx5CVMAu5xszngi85SSOgzJwZtJHeLHDhDmw/rq8KKTa5Ai/gkCXNCymA/FEejqFxYliKhrCgRcHN6LYSmfL7GYoFIPghAV/N5C3bkhts/PoA+a+A0Pa86ALZSxjuhCm3dNMnk63otEjeyU8UBazwwr9Kzjofhw55WunbTEKduPI54maPsnb7FA2IiUMvILpCvpalKi37s4mFhWns2ICmVbRrp+BZqf3 ecampohermoso@MacBook-Pro-de-Ernesto.local
```

### Sistemas Operativos serios: *NIX

Para verificar si ya tienes una llave RSA para conectarte por SSH, puedes seguir estos pasos:

1.  Abre una terminal o línea de comandos en tu sistema operativo.
    
2.  Escribe el siguiente comando y presiona Enter:
    
    ```
    ls -al ~/.ssh/id_rsa
    ```
    
3.  Si aparece un mensaje que indica que el archivo no existe, significa que no tienes una llave RSA. En caso contrario, significa que ya tienes una llave RSA.
    

En caso de que no tengas una llave RSA, puedes generar una nueva sin contraseña siguiendo estos pasos:

1.  Abre una terminal o línea de comandos en tu sistema operativo.
    
2.  Escribe el siguiente comando y presiona Enter:
    
    ```
    ssh-keygen -t rsa -b 4096
    
    ```
    
3.  Presiona Enter para aceptar la ubicación predeterminada del archivo de la llave.
    
4.  Presiona Enter para dejar la contraseña en blanco.
    
5.  Presiona Enter nuevamente para confirmar que no deseas establecer una contraseña.
    
6.  La llave RSA se habrá generado y se habrá guardado en el directorio `~/.ssh/id_rsa`.

7.  Para obtener la llave publica ejecuta lo siguiente: `cat ~/.ssh/id_rsa.pub`

## Creamos un Dorplet (Maquina Virtual)

Un Droplet es una instancia de servidor virtual en la nube que puede ser utilizada para alojar aplicaciones, sitios web y otros servicios en línea. A continuación, se detallan los pasos para crear un Droplet:

1.  Inicia sesión con la cuenta creada previamente.
    
2.  Iniciar sesión en tu cuenta: Una vez que hayas confirmado tu correo electrónico, inicia sesión en tu cuenta de Digital Ocean con tu dirección de correo electrónico y contraseña.
    
3.  Acceder al panel de control: Después de iniciar sesión, serás redirigido al panel de control de Digital Ocean.
    
4.  Crear un nuevo Droplet: Haz clic en el botón "Create" (Crear) en la esquina superior derecha y selecciona "Droplets" en el menú desplegable.
    
5.  Elegir la imagen del sistema operativo: En la sección "Choose an image" (Elegir una imagen), selecciona el sistema operativo que deseas utilizar en tu Droplet. Puedes elegir entre varias distribuciones de Linux o incluso subir tu propia imagen personalizada.
    
6.  Elegir el plan y tamaño del Droplet: En la sección "Choose a plan" (Elegir un plan), selecciona el plan que mejor se adapte a tus necesidades. Digital Ocean ofrece planes que varían en precio, RAM, almacenamiento y transferencia de datos. Luego, en la sección "Choose a size" (Elegir un tamaño), selecciona el tamaño de Droplet que mejor se ajuste a tus requisitos.
    
7.  Elegir la región del centro de datos: En la sección "Choose a datacenter region" (Elegir una región del centro de datos), selecciona la ubicación geográfica del centro de datos donde se alojará tu Droplet. Es recomendable elegir una región cercana a la mayoría de tus usuarios para reducir la latencia.
    
8.  Configurar opciones adicionales: En la sección "Select additional options" (Seleccionar opciones adicionales), puedes activar características adicionales como monitoreo, copias de seguridad automáticas, IPv6 y más, según tus necesidades.
    
9.  Agregar tus claves SSH: En la sección "Authentication" (Autenticación), puedes elegir entre utilizar una contraseña o una clave SSH para acceder a tu Droplet. Se recomienda utilizar claves SSH, ya que son más seguras. Si aún no has agregado una clave SSH a tu cuenta, sigue las instrucciones proporcionadas para hacerlo.
    
10.  Establecer un nombre de host y etiquetas: En la sección "Finalize and create" (Finalizar y crear), asigna un nombre de host a tu Droplet y agrega etiquetas si lo deseas. Las etiquetas son útiles para organizar y gestionar tus recursos en Digital Ocean.
    
11.  Crear el Droplet: Haz clic en el botón "Create Droplet" (Crear Droplet) en la parte inferior de la página. Digital Ocean creará tu Droplet en unos minutos.
    
12.  Conectar al Droplet: Una vez que tu Droplet esté listo, recibirás un correo electrónico con la dirección IP. Utiliza un cliente SSH y la dirección IP proporcionada para conectarte a tu Droplet. Si configuraste la autenticación con clave SSH, asegúrate de utilizar la clave privada correspondiente.

Ya has creado un Droplet en Digital Ocean y puedes comenzar a usarlo para alojar tus aplicaciones, sitios web o cualquier otro servicio que desees. Asegúrate de mantener tus sistemas actualizados y de seguir las mejores prácticas de seguridad para proteger tus recursos en la nube.

## Instalar Docker en el Droplet recien creado.

Conectate al Droplet recien creado y sigue las instrucciones de:

https://docs.docker.com/engine/install/ubuntu/

De todas formas se da un breve resumen:

### Uninstall old versions[🔗](https://docs.docker.com/engine/install/ubuntu//#uninstall-old-versions)

Older versions of Docker went by the names of `docker`, `docker.io`, or `docker-engine`, you might also have installations of `containerd` or `runc`. Uninstall any such older versions before attempting to install a new version:

```
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

`apt-get` might report that you have none of these packages installed.

Images, containers, volumes, and networks stored in `/var/lib/docker/` aren’t automatically removed when you uninstall Docker. If you want to start with a clean installation, and prefer to clean up any existing data, read the [uninstall Docker Engine](https://docs.docker.com/engine/install/ubuntu//#uninstall-docker-engine) section.

### Install using the apt repository[🔗](https://docs.docker.com/engine/install/ubuntu//#install-using-the-repository)

Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

#### Set up the repository

1.  Update the `apt` package index and install packages to allow `apt` to use a repository over HTTPS:
    
    ```
    $ sudo apt-get update
    
    $ sudo apt-get install \
        ca-certificates \
        curl \
        gnupg
    ```
    
2.  Add Docker’s official GPG key:
    
    ```
    $ sudo install -m 0755 -d /etc/apt/keyrings
    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    $ sudo chmod a+r /etc/apt/keyrings/docker.gpg
    ```
    
3.  Use the following command to set up the repository:
    
    ```
    $ echo \
      "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
      "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```
    

#### Install Docker Engine

1.  Update the `apt` package index:
    
    ```
    $ sudo apt-get update
    ```
    
2.  Install Docker Engine, containerd, and Docker Compose.
    
    -   Latest
    -   Specific version
    
      
    
    To install the latest version, run:
    
    ```
     $ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```
    
    
3.  Verify that the Docker Engine installation is successful by running the `hello-world` image:
    
    ```
    $ sudo docker run hello-world
    ```
    
    This command downloads a test image and runs it in a container. When the container runs, it prints a confirmation message and exits.
    

You have now successfully installed and started Docker Engine.

## Ejecutar Neo4J

1. Descargamos la imagen:

```bash
docker run --publish=7474:7474 --publish=7687:7687  -d   neo4j
```

3. Buscamos nuestra IP publica en el panel de Digital Ocean.

4. Nos conectamos a Neo4J
  - Abrir: http://LA_IP_DE_DIGITAL_OCEAN:7474.
  - Ingresar con:
    - Usuario: neo4j
    - Password: neo4j
  - Cambiar la contraseña.
  - Ejecutar: `:play start`
  - Clic en "Open Guide"
  - Realizar los pasos de la guía completa



