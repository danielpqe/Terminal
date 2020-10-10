# Command Line
- cat: Nos muestra el contenido completo de un archivo
ejemplo: cat tables.txt
- head: Nos muestra las primeras lineas (También podemos escoger cuantas lineas queremos utilizando el modificador [-n #]).
Ejemplos:
head tables.txt
head -n 5 tables.txt
- tail: Muestras las ultimas lineas del final (Inverso a head, tambien le funciona modificadores)
Ejemplos:
tailtables.txt
tail -n 5 tables.txt
## Utilidades Batch Avanzadas:
- grep: Permite trabajar con expresiones regulares, funciona como un buscador dentro del archivo.
Ejemplos:
`grep hanks dump1.sql` = [comando][expresión regular][archivo]
Para buscar sin importar si esta en mayuscula o miniscula:
`grep -i hanks dump1.sql`
_Tambien podemos buscar una expresión de una frase que termine con la misma palabra que estemos buscando:
`grep -i “hanks’),$”`
- sed: Screem Editor, tratamiento de flujos de caracteres. Este comando nos permite reemplazar una expresión por otra.
ejemplos:
`sed ‘s/hanks/selleck/g’ dump1.sql` = [comando][subcomando- sustitución][expresión original][nueva expresión][modificador-(/g de global, indica que tiene que hacerse a lo largo de todo el flujo)][Indicar cual es el flujo a utilizar (Archivo de texto)]
SED no modifica el archivo, lo que hace es crear un nuevo flujo con la modificación
Para eliminar la ultima linea podemos utilizar:
    `sed ‘$d’ nuevasPelis.csv` = [Comando][’$sub-comando’][archivo]
- awk: Trataminento de texto delimitado, este comando sirve para trabajar con archivos de textos delimitados por comas.
Ejemplos:
`awk -F ‘;’ ‘{ print $1}’ nuevasPelis.csv`

## Comunicación entre procesos
- Redireccionar la entrada de un comando con el contenido de un archivo

    `$ nombre_comando<nombre_archivo`
- Redireccionar la salida de un comando agregando reescribiendo el contenido del archivo txt

    `$ ls -l > archivo.txt`

- Redireccionar la salida de un comando agregandolo al final del contenido del archivo txt

    `$ ls -l >> archiv.txt`

- Concatenación de comandos (Pipelines)
    - Mostrar el contenido de un comando en secciones (Enter: linea a linea, Espacio: sección a sección) 

        `$ comando | more`
    - Cantidad de caracteres, palabras o lineas del resultado del comando

        `$comando | wc`

## Administración de procesos en background y foreground
- Ejecución en primer plano: Solo se ejecuta un proceso a la vez

- Ejecución en background: El proceso se ejecuta en segundo plano mientras el control regresar inmediatamente, otra opción (Ctrl+z)
    `$ mysql -h 127.0.0.1 -u root -p1234 <dump1.sql &`

    Traer al primer plano un comando que se esta ejecutando en segundo plano
    `$ fg`
- Demonios: Procesos que siempre estan ejecutandose ya que los programas los usan

- Listar procesos
    `$ps`, `$top`
- Cómo detener procesos
    Ctrl+c
    kill -9 numero_proceso (9: máxima prioridad)
    killall -numero_prioridad nombre_ejecutable

## Permisos sobre archivos

- Modificar los permisos de un archivo o directorio

    `$ chmod ugo +- rwx file_name`
    `$ chmod 670 rwx file_name `

- Cambiar el owner del archivo por otro usuario, para ejecutarlo se necesita permisos root

    `$ sudo chown user_name file_name`

- Cambiar el grupo al que pertenece un archivo, para ejecutarlo se necesita permisos root

    `$ sudo chgrp group_name file_name`

## Sistema de manejo de paquetes
Sirve para instalar software al pc, un manejador de paquetes gestiona las dependencias del software, analiza que esta instalado, que falta instalar y las configuraciones necesarias (apt, zypper, rpm)

    - pip: python

    - composer: php

    - npm: nodejs


`$sudo install pip pandas`

`npm install react`

## Herramientas de compresión y combinación de archivos
- .gz: Comprimir
    - Comprimir: gzip archivo.txt
    - Descomprimir: gzip -d archivo.txt.gz
 
- .tar: Combinar, el tamaño es el mismo
    - Empaquetar: tar cf paquete.tar /carpeta/a/empaquetar/
    - Ver contenido del paquete: tar tf paquete.tar
    - Empaquetar y ver contenido empaquetado: tar -cvf paquete.tar /carpeta/a/empaquetar/
    - Desempaquetar: tar xf paquete.tar
 
- .tar.gz: Combinar y comprimir
    - Empaquetar y Comprimir: tar czf empaquetado.tar.gz /carpeta/a/empaquetar/y/comprimir
    - Descomprimir: tar xzf archivo.tar.gz

## Herramientas de búsqueda de archivos
- Locate: Busca en todo el sistema de archivos solo ingresando el nombre del archivo, trabaja con una base de datos que hay que actualizar periodicamente para encontrar nuevos archivos
    `$ locate helloworld.php`
    `$ sudo updatedb`

- Whereis: Para ubicar archivos binarios (Comandos)
    `$whereis echo`

- find: Más compleja, busca dentro de un arbol de directorios ingresando unos parametros
    `$ find . -user daniel -perm 644`: Buscar archivos que se encuentren en el directorio actual que le pertenezcan a daniel y que tengan permisos 644

    `$ find . -type f -mtime +7`: Buscar solo archivos modificados hace 7 dias

    `find . type -f mtime +7 -exec cp {} ./backup/ \;`: Permite ejecutar acciones sobre el resultado de cada línea o archivo devuelto por find

## Herramientas para interactuar a través de HTTP
- Curl: Sirve para realizar pedidos, crudos, a un servidor

    `$curl https://fast.com`

- wget: Para descargar archivos binarios desde servidores

    `$wget https://wordpress.org/latest.zip`

## Acceso seguro a otras computadoras

- ssh: Secure shell (Terminal segura),Con este comando ingresamos a un servidod de manera segura.
    ejemplo: ssh leeway -prod

- mail: Nos permite enviar un email desde el servidor. Para que este comando funcione hay que tener algunas cosas configuradas

    Ejemplo: echo “Probando” | mail -s(-s: es el asunto del correo) “Probando para platzi”

## Qué son y cómo se utilizan las variables de entorno

Definición global a la que todos los procesos tienen acceso
- echo $PATH = se encuentran todos los comandos ejecutables
- Asignación de las variables de entorno
    - export: Este comando se utiliza para asignar a toda la sesión
    Ejemplo: export MI_VAR = mauro, si luego escribimos echo $MI_VAR se mostrará mauro en la terminal. (Este permanecerá miestras dure mi sesión)
- var: Este comando solo asigna el valor para el proximo proceso que se va a ejecutar. este no es muy usual.
    Ejemplo: MI_VAR=/home php env.php

## Automatización de tareas

Ejecución de tareas progragamdas usando scripts en bash

- at: Programar una tarea que se ejecuta segun un timer

    `$ at now + 2 minutes`
    `$ at> echo "Mensaje" > ~/tarea.txt`

    Ctrl+d para terminar la programación

- cron: Programar tareas para que se ejecuten de forma periódica según el siguiente formato:

    `minuto hora dia mes dia_semana comando`
    
    `0 18 * * * echo "Hola" > hola.txt `