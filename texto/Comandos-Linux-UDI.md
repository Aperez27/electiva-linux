# Comandos-Linux-UDI

## Diapositiva 1

- GNU/LINUX
- Gestión de archivos, directorios, usuarios y grupos
- Comandos esenciales · caso de estudio · glosario
- Ing. Angelmiro Quiroz Parra
- aparra19@udi.edu.co
- 1

## Diapositiva 2

- CONTENIDO
- Navegación y gestión de directorios
- Manipulación, lectura y búsqueda de archivos
- Usuarios, grupos y propiedad
- Permisos básicos y especiales
- Caso de estudio: laboratorio del semillero
- Glosario de comandos
- 2

## Diapositiva 3

- DIRECTORIOS
- Navegar y organizar el sistema de ficheros
- 3

## Diapositiva 4

- Navegación entre directorios
- Comando
- Función
- pwd
- Muestra la ruta del directorio de trabajo
- cd /var/log
- Entra en el directorio indicado
- cd .. · cd ../..
- Retrocede uno o dos niveles
- cd - · cd ~user1
- Regresa al directorio anterior · va al home de user1
- ls -la
- Lista todo, incluidos ocultos (-a), con detalles (-l)
- ls -lh · ls -F
- Tamaños legibles y permisos · marca el tipo de cada entrada
- tree
- Muestra ficheros y carpetas en forma de árbol
- Fuente: Guía de referencia de comandos Linux; Wiki de GUTL, «Más de 400 comandos para GNU/Linux».
- 4

## Diapositiva 5

- Crear y eliminar directorios
- Sintaxis
- Comportamiento
- Ejemplo
- mkdir dir
- Crea una carpeta vacía
- mkdir docs
- mkdir d1 d2 d3
- Crea varias carpetas a la vez
- mkdir img notas
- mkdir -p ruta
- Crea la estructura anidada y los padres que falten
- mkdir -p /tmp/a/b
- mkdir "mi dir"
- Nombres con espacios: comillas o barra invertida
- mkdir "mis docs"
- rmdir dir
- Elimina una carpeta solo si está vacía
- rmdir vacia
- rmdir -p ruta
- Elimina de forma ascendente si quedan vacías
- rmdir -p a/b/c
- rm -r dir
- Borra una carpeta con todo su contenido
- rm -r proyecto_old
- rm -rf dir
- Igual que -r, pero sin pedir confirmación
- rm -rf cache_dir
- Fuente: Guía de referencia de comandos Linux; Wiki de GUTL, «Más de 400 comandos para GNU/Linux».
- 5

## Diapositiva 6

- rm -rf
- borra directorios y su contenido de forma definitiva, sin pasar por la papelera. Verifica siempre la ubicación con
- pwd
- antes de ejecutarlo.
- Advertencia de seguridad · Guía de referencia de comandos Linux
- 6

## Diapositiva 7

- ARCHIVOS
- Crear, copiar, mover, leer y buscar archivos
- 7

## Diapositiva 8

- Manipulación de archivos
- Sintaxis
- Comportamiento
- Ejemplo
- touch archivo
- Crea un archivo vacío o actualiza su fecha
- touch index.html
- cp origen destino
- Copia un archivo
- cp notas.txt copia.txt
- cp -r · cp -a
- Copia directorios (recursivo · conserva atributos)
- cp -r /app /backup/app
- mv origen destino
- Mueve o renombra archivos y carpetas
- mv foto.jpg foto_old.jpg
- ln -s objetivo enlace
- Crea un enlace simbólico (acceso directo)
- ln -s /var/www/html web
- ln objetivo enlace
- Crea un enlace físico al mismo contenido
- ln file1 lnk1
- file archivo
- Informa el tipo de contenido del archivo
- file informe.pdf
- rm -f archivo
- Borra un archivo sin pedir confirmación
- rm -f file1
- Fuente: Guía de referencia de comandos Linux; Wiki de GUTL, «Más de 400 comandos para GNU/Linux».
- 8

## Diapositiva 9

- Consultar el contenido y el tamaño
- Sintaxis
- Comportamiento
- Ejemplo
- cat archivo
- Muestra el contenido completo
- cat /etc/hosts
- tac archivo
- Muestra el contenido en orden inverso
- tac registro.txt
- less archivo
- Navega el archivo de forma interactiva
- less /var/log/syslog
- head archivo
- Lee las primeras líneas
- head -n 5 datos.csv
- tail -f archivo
- Lee las últimas líneas y sigue los cambios
- tail -f /var/log/syslog
- du -sh dir
- Estima el espacio que ocupa un directorio
- du -sh dir1
- Fuente: Guía de referencia de comandos Linux; Wiki de GUTL, «Más de 400 comandos para GNU/Linux».
- 9

## Diapositiva 10

- Buscar archivos y texto
- Sintaxis
- Qué encuentra
- find /home -name '*.pdf'
- Archivos por nombre o patrón
- find /ruta -type f | d
- Solo archivos (f) o solo directorios (d)
- find / -user user1
- Elementos que pertenecen a un usuario
- find /usr/bin -type f -mtime -10
- Archivos modificados en los últimos 10 días
- locate '*.ps'
- Búsqueda rápida en el índice creado con updatedb
- grep -rn 'ERROR' /var/log/
- Líneas que contienen un patrón, con número de línea
- which python3 · whereis halt
- Ruta del ejecutable · binario, fuentes y manual
- Combinación con tubería: find /var/log -type f | grep '.log' | wc -l cuenta los archivos de registro.
- Fuente: Guía de referencia de comandos Linux; Wiki de GUTL, «Más de 400 comandos para GNU/Linux».
- 10

## Diapositiva 11

- USUARIOS Y GRUPOS
- Cuentas, grupos y propiedad de los archivos
- 11

## Diapositiva 12

- sudo y su: privilegios de root
- Crear usuarios, cambiar dueños o permisos del sistema exige privilegios de root.
- Sintaxis
- Función
- Ejemplo
- sudo comando
- Ejecuta un comando como root con la contraseña propia
- sudo useradd ana
- sudo -u usuario comando
- Ejecuta un comando como otro usuario
- sudo -u ana ls ~ana
- sudo -i
- Abre una shell de root con su entorno
- sudo -i
- sudo -l
- Lista lo que el usuario tiene permitido ejecutar
- sudo -l
- su usuario
- Cambia de usuario; pide la contraseña del destino
- su ana
- su -
- Cambia a root cargando su entorno completo
- su -
- exit
- Cierra la sesión abierta con su o sudo -i
- exit
- sudo eleva un comando puntual y lo registra; su cambia la identidad de toda la sesión. Solo usan sudo los usuarios autorizados en /etc/sudoers.
- 12

## Diapositiva 13

- Administración de usuarios
- Sintaxis
- Función
- useradd user1
- Crea un nuevo usuario
- useradd -c "Nombre" -g admin -d /home/user1 -s /bin/bash user1
- Crea un usuario con comentario, grupo, home y shell
- usermod -c "User FTP" -g system -s /bin/nologin user1
- Cambia los atributos de una cuenta
- userdel -r user1
- Borra el usuario y su directorio home (-r)
- passwd · passwd user1
- Cambia la contraseña propia · la de otro (solo root)
- chage -E 2026-12-31 user1
- Fija la fecha de caducidad de la cuenta
- pwck
- Verifica el formato de /etc/passwd y los usuarios
- Fuente: Wiki de GUTL, «Más de 400 comandos para GNU/Linux», sección Usuarios y grupos.
- 13

## Diapositiva 14

- Administración de grupos
- Sintaxis
- Función
- groupadd devs
- Crea un grupo
- groupdel devs
- Elimina un grupo
- groupmod -n nuevo viejo
- Renombra un grupo
- usermod -g devs carlos
- Asigna o cambia el grupo primario de una cuenta
- newgrp devs
- Cambia el grupo predeterminado de los archivos que se creen en la sesión
- grpck
- Verifica el formato de /etc/group y los grupos
- Fuente: Guía de referencia de comandos Linux; Wiki de GUTL, «Más de 400 comandos para GNU/Linux».
- 14

## Diapositiva 15

- Propiedad de archivos
- Sintaxis
- Función
- Ejemplo
- chown usuario f
- Cambia solo el propietario
- chown juan nota.txt
- chown u:grupo f
- Cambia propietario y grupo a la vez
- chown maria:admin script.py
- chown :grupo f
- Cambia solo el grupo y conserva el usuario
- chown :devs proyecto.tar
- chown -R u dir
- Aplica el cambio a todo el contenido
- chown -R www-data /var/www
- chgrp grupo f
- Comando dedicado a cambiar el grupo
- chgrp estudiantes tarea.doc
- Fuente: Guía de referencia de comandos Linux, sección 4.
- 15

## Diapositiva 16

- Propiedad: usuario y grupo propietario
- Dos dueños
- Cada archivo y directorio tiene un usuario propietario y un grupo propietario, visibles en
- ls -l
- .
- Privilegios
- Por seguridad, cambiar el dueño de un archivo suele requerir root o
- sudo
- .
- chown o chgrp
- chown
- cambia usuario, grupo o ambos;
- chgrp
- es el comando dedicado solo al grupo.
- sudo chown usuario1:grupo1 archivo1
- El separador «:» actualiza ambos atributos a la vez
- sudo chown :grupo1 archivo1
- Sin usuario antes de «:», solo cambia el grupo
- sudo chgrp grupo1 archivo1
- Resultado equivalente con el comando dedicado
- Fuente: documento «Gestión de propiedad Linux».
- 16

## Diapositiva 17

- PERMISOS
- Quién puede leer, escribir y ejecutar
- 17

## Diapositiva 18

- Cómo se leen los permisos
- Lectura · r
- Valor 4
- Ver el contenido del archivo o listar el directorio.
- Escritura · w
- Valor 2
- Modificar el archivo o crear y borrar entradas en el directorio.
- Ejecución · x
- Valor 1
- Ejecutar el archivo o entrar en el directorio con cd.
- -rwxr-xr-x
- Propietario u = rwx (7) · grupo g = r-x (5) · otros o = r-x (5) → 755
- -rw-r--r--
- Propietario lee y escribe (6 = 4 + 2) · grupo y otros solo leen (4) → 644
- 18

## Diapositiva 19

- Anatomía de la cadena de permisos
- ls -l muestra 10 caracteres: tipo de elemento y tres bloques de permisos.
- -
- Tipo
- carácter 1
- rwx
- Propietario · u
- caracteres 2–4
- r-x
- Grupo · g
- caracteres 5–7
- r--
- Otros · o
- caracteres 8–10
- Primer carácter
- -
- archivo normal ·
- d
- directorio ·
- l
- enlace simbólico
- Lectura del ejemplo
- Dueño con rwx, grupo lee y ejecuta, otros solo leen. El guion indica permiso no concedido.
- Fuente: documento «Permisos Linux: chmod».
- 19

## Diapositiva 20

- Cambiar permisos: chmod y umask
- Sintaxis
- Modo
- Efecto
- chmod a+r nota.txt
- Simbólico
- Lectura para todos (a = all)
- chmod ugo+rwx public/
- Simbólico
- Lectura, escritura y ejecución a los tres roles
- chmod go-rwx privado/
- Simbólico
- Revoca todo al grupo y a otros
- chmod -R 755 /var/www
- Octal recursivo
- u = rwx, g = r-x, o = r-x en todo el árbol
- chmod 644 config.conf
- Octal
- Dueño lee y escribe; grupo y otros solo leen
- chmod 777 script.sh
- Octal
- Control total para todos; evitar en producción
- umask 022
- Máscara
- Archivos nuevos nacen con 644 y directorios con 755
- Fuente: Guía de referencia de comandos Linux, secciones 2 y 4.
- 20

## Diapositiva 21

- Modo simbólico y modo octal
- Simbólico: rol + operador + permiso
- Rol
- u propietario · g grupo · o otros · a todos
- Operador
- + añadir · - quitar
- Permiso
- r lectura · w escritura · x ejecución
- chmod a+r archivo.txt
- chmod go-rwx carpeta
- chmod -R ugo+rwx carpeta
- -R aplica el cambio a todo el contenido del directorio.
- Octal: suma de r = 4, w = 2, x = 1
- Valor
- Suma
- Permisos
- 7
- 4 + 2 + 1
- rwx
- 6
- 4 + 2
- rw-
- 5
- 4 + 1
- r-x
- 4
- 4
- r--
- 0
- —
- ---
- Tres dígitos: propietario, grupo, otros. chmod 755 = rwxr-xr-x.
- Fuente: documento «Permisos Linux: chmod».
- 21

## Diapositiva 22

- Tabla de permisos en octal
- Valor
- rwx
- Significado
- 0
- ---
- Sin acceso
- 1
- --x
- Ejecución
- 2
- -w-
- Escritura
- 3
- -wx
- Escritura y ejecución
- 4
- r--
- Lectura
- 5
- r-x
- Lectura y ejecución
- 6
- rw-
- Lectura y escritura
- 7
- rwx
- Lectura, escritura y ejecución
- Regla
- 3 números: usuario, grupo y otros. Cada uno es una suma de:
- 4 = r
- 2 = w
- 1 = x
- Ejemplos
- rw-r--r--
- →
- 644
- rwxrwxrwx
- →
- 777
- --x--x--x
- →
- 111
- Fuente: documento «Permisos Linux: chmod».
- 22

## Diapositiva 23

- Permisos y atributos especiales
- Permiso
- Notación
- Funcionamiento
- Ejemplo
- SUID
- u+s · 4000
- Ejecuta el binario con privilegios del propietario; ls -l muestra rwsr-xr-x
- chmod 4755 /bin/fichero
- SGID
- g+s · 2000
- En carpetas, los archivos nuevos heredan el grupo del directorio
- chmod 2775 /home/public
- Sticky bit
- o+t · 1000
- En carpetas públicas, solo el dueño borra sus archivos; muestra t en otros
- chmod 1777 /tmp/compartido
- Inmutable
- chattr +i
- El archivo no se puede borrar, alterar, renombrar ni enlazar
- chattr +i file1
- Auditoría: find / -perm -u+s lista todos los archivos con SUID. El signo «-» retira el permiso: chmod g-s.
- Fuente: Guía de referencia de comandos Linux; Wiki de GUTL, «Más de 400 comandos para GNU/Linux».
- 23

## Diapositiva 24

- SUID, SGID y sticky bit en detalle
- SUID
- El binario se ejecuta con los privilegios del propietario, a menudo root.
- Caso de uso: passwd modifica /etc/shadow, que pertenece a root.
- chmod u+s · quitar u-s
- Octal 4755
- En ls -l rwsr-xr-x
- SGID
- En archivos, corre con privilegios del grupo; en directorios, lo nuevo hereda el grupo padre.
- Caso de uso: carpetas colaborativas de un equipo.
- chmod g+s · quitar g-s
- Octal 2775
- En ls -l rwxr-sr-x
- Sticky bit
- En directorios públicos, solo el dueño del archivo, el del directorio o root pueden borrarlo.
- Caso de uso: el directorio /tmp.
- chmod o+t · quitar o-t
- Octal 1777
- En ls -l rwxrwxrwt
- Fuente: documento «Permisos especiales Linux».
- 24

## Diapositiva 25

- Notación octal de 4 dígitos
- Sintaxis: chmod ESPECIAL U G O archivo . El primer dígito suma los permisos especiales activos.
- Valor
- Permiso especial
- Ejemplo
- Resultado
- 4
- SUID
- chmod 4755
- SUID + rwxr-xr-x
- 2
- SGID
- chmod 2775
- SGID + rwxrwxr-x
- 1
- Sticky bit
- chmod 1777
- Sticky + rwxrwxrwx
- Una S o T en mayúscula en ls -l indica que el permiso especial está activo, pero falta el permiso de ejecución x subyacente.
- Fuente: documento «Permisos especiales Linux».
- 25

## Diapositiva 26

- CASO DE ESTUDIO
- Configurar el servidor del laboratorio del semillero
- 26

## Diapositiva 27

- Planteamiento del caso
- Un semillero recibe un servidor Linux y necesita un espacio de trabajo compartido, ordenado y seguro en /srv/semillero.
- Equipo
- ana · coordinadora, grupo devs
- carlos · desarrollador, grupo devs
- luis · practicante, grupo revisores
- Estructura
- codigo/
- docs/
- entregas/
- actas/
- Reglas
- Código editable solo por devs
- Documentos visibles para todos
- Nadie borra entregas ajenas
- Actas privadas de la coordinadora
- 27

## Diapositiva 28

- Caso de estudio · paso 1
- Crear usuarios y grupos
- sudo groupadd devs
- Grupo del equipo de desarrollo
- sudo groupadd revisores
- Grupo de quienes revisan entregas
- sudo useradd -m -c "Ana Rojas" -g devs -s /bin/bash ana
- Coordinadora con home y shell
- sudo useradd -m -g devs carlos
- Desarrollador
- sudo useradd -m -g revisores luis
- Practicante
- sudo passwd ana
- Asigna contraseña (repetir por usuario)
- sudo chage -E 2026-12-31 luis
- La cuenta del practicante caduca
- sudo pwck ; sudo grpck
- Valida /etc/passwd y /etc/group
- La opción -m de useradd crea el directorio home si no existe.
- 28

## Diapositiva 29

- Caso de estudio · paso 2
- Construir directorios y archivos
- sudo mkdir -p /srv/semillero
- Crea la ruta con sus padres
- cd /srv/semillero ; pwd
- Entra y confirma la ubicación
- sudo mkdir codigo docs entregas "actas de reunion"
- Cuatro carpetas a la vez
- sudo mv "actas de reunion" actas
- Renombra para evitar espacios
- sudo touch docs/README.txt codigo/main.py
- Archivos iniciales vacíos
- sudo cp docs/README.txt docs/GUIA.txt
- Copia base para la guía
- sudo ln -s /srv/semillero/entregas /home/luis/entregas
- Acceso directo en el home de luis
- tree /srv/semillero
- Revisa el árbol resultante
- 29

## Diapositiva 30

- Caso de estudio · paso 3
- Asignar propiedad y permisos
- sudo chown -R ana:devs /srv/semillero
- Ana es dueña; devs, el grupo
- sudo chmod -R 755 /srv/semillero
- Base: lectura para todos
- sudo chmod 2775 codigo
- SGID: lo nuevo hereda el grupo devs
- sudo chgrp revisores entregas
- Las entregas pasan a revisores
- sudo chmod 1777 entregas
- Sticky bit: cada quien borra solo lo suyo
- sudo chmod go-rwx actas
- Actas privadas: queda en 700
- sudo chmod 644 docs/README.txt docs/GUIA.txt
- Documentos de solo lectura
- umask 002
- En la sesión de devs: archivos 664, carpetas 775
- 30

## Diapositiva 31

- Caso de estudio · paso 4
- Verificar y mantener
- ls -la /srv/semillero
- Comprueba dueños, grupos y permisos
- find /srv/semillero -type f -name '*.py'
- Localiza el código fuente
- grep -rn 'TODO' /srv/semillero/codigo
- Tareas pendientes en el código
- du -sh /srv/semillero/entregas
- Espacio que ocupan las entregas
- sudo usermod -g devs luis
- Luis se une al desarrollo
- sudo find / -user luis
- Inventario de sus archivos antes de la baja
- sudo userdel -r luis
- Fin de la práctica: cuenta y home fuera
- sudo chgrp devs entregas ; sudo groupdel revisores
- Reasigna la carpeta y elimina el grupo vacío
- 31

## Diapositiva 32

- Resultado de ls -la tras el paso 3
- Carpeta
- Permisos
- Octal
- Dueño:grupo
- Efecto
- codigo
- drwxrwsr-x
- 2775
- ana:devs
- devs edita; hereda grupo
- docs
- drwxr-xr-x
- 755
- ana:devs
- Todos leen; solo ana escribe
- entregas
- drwxrwxrwt
- 1777
- ana:revisores
- Todos depositan; nadie borra lo ajeno
- actas
- drwx------
- 700
- ana:devs
- Solo la coordinadora
- Fuente: elaboración propia a partir de los comandos del caso de estudio.
- 32

## Diapositiva 33

- Retos para poner a prueba el caso
- ¿Puede carlos borrar una entrega de luis?
- ¿Qué grupo recibe un archivo nuevo en codigo?
- ¿Por qué falla rmdir docs y qué alternativa existe?
- ¿Puede luis entrar en actas?
- ¿Cómo proteger README.txt incluso frente a root?
- ¿Cómo auditar binarios con SUID en el servidor?
- 33

## Diapositiva 34

- Respuestas de los retos
- N.º
- Respuesta
- Comando de comprobación
- 1
- No: el sticky bit solo permite borrar al dueño
- ls -ld entregas
- 2
- devs, por el SGID de la carpeta
- touch codigo/a.py ; ls -l codigo
- 3
- docs no está vacía; se usa rm -r tras revisar
- pwd ; sudo rm -r docs
- 4
- No: con 700 grupo y otros no tienen x
- ls -ld actas
- 5
- Atributo inmutable; se retira con chattr -i
- sudo chattr +i docs/README.txt
- 6
- Buscar el permiso u+s en todo el sistema
- find / -perm -u+s
- 34

## Diapositiva 35

- GLOSARIO
- 41 comandos: función y sintaxis
- 35

## Diapositiva 36

- Glosario · cat a cp
- Comando
- Función
- Sintaxis
- cat
- Muestra el contenido completo de un archivo
- cat archivo
- cd
- Cambia el directorio de trabajo
- cd [ruta | .. | - | ~usuario]
- chage
- Fija la caducidad de una cuenta
- chage -E AAAA-MM-DD usuario
- chattr
- Asigna atributos especiales (+i inmutable, +a solo añadir)
- chattr [+|-]atributo archivo
- chgrp
- Cambia el grupo propietario
- chgrp [-R] grupo archivo
- chmod
- Modifica permisos en modo simbólico u octal
- chmod [-R] modo archivo
- chown
- Cambia propietario y, opcionalmente, grupo
- chown [-R] usuario[:grupo] archivo
- cp
- Copia archivos o directorios
- cp [-r | -a] origen destino
- 36

## Diapositiva 37

- Glosario · du a grpck
- Comando
- Función
- Sintaxis
- du
- Estima el espacio usado por un directorio
- du -sh directorio
- file
- Indica el tipo de contenido de un archivo
- file archivo
- find
- Busca por nombre, tipo, usuario, fecha o permisos
- find ruta [-name | -type | -user | -perm] valor
- grep
- Filtra las líneas que coinciden con un patrón
- grep [-rn] 'patrón' archivo
- groupadd
- Crea un grupo
- groupadd grupo
- groupdel
- Elimina un grupo
- groupdel grupo
- groupmod
- Renombra un grupo
- groupmod -n nuevo viejo
- grpck
- Verifica el formato de /etc/group
- grpck
- 37

## Diapositiva 38

- Glosario · head a newgrp
- Comando
- Función
- Sintaxis
- head
- Muestra las primeras líneas de un archivo
- head [-n N] archivo
- less
- Navega un archivo de forma interactiva
- less archivo
- ln
- Crea enlaces físicos o simbólicos (-s)
- ln [-s] objetivo enlace
- locate
- Busca en el índice generado por updatedb
- locate patrón
- ls
- Lista contenido: -l detalles, -a ocultos, -h tamaños
- ls [-lahF] [ruta]
- mkdir
- Crea directorios; -p crea los padres
- mkdir [-p] dir1 [dir2 …]
- mv
- Mueve o renombra archivos y directorios
- mv origen destino
- newgrp
- Cambia el grupo activo de la sesión
- newgrp grupo
- 38

## Diapositiva 39

- Glosario · passwd a tail
- Comando
- Función
- Sintaxis
- passwd
- Cambia la contraseña propia o de otro (root)
- passwd [usuario]
- pwck
- Verifica el formato de /etc/passwd
- pwck
- pwd
- Muestra la ruta del directorio actual
- pwd
- rm
- Borra archivos; -r directorios, -f sin confirmar
- rm [-r] [-f] ruta
- rmdir
- Borra directorios vacíos
- rmdir [-p] directorio
- su
- Cambia de usuario en la sesión actual
- su [-] [usuario]
- sudo
- Ejecuta un comando con privilegios de otro usuario (root por defecto)
- sudo [-u usuario] comando
- tac
- Muestra un archivo en orden inverso
- tac archivo
- tail
- Muestra las últimas líneas; -f sigue los cambios
- tail [-f] [-n N] archivo
- 39

## Diapositiva 40

- Glosario · touch a which
- Comando
- Función
- Sintaxis
- touch
- Crea un archivo vacío o actualiza su fecha
- touch [-t AAMMDDhhmm] archivo
- tree
- Muestra directorios y archivos en árbol
- tree [ruta]
- umask
- Define la máscara de permisos por defecto
- umask [máscara]
- useradd
- Crea una cuenta de usuario
- useradd [-m] [-c "com"] [-g grupo] [-d home] [-s shell] usuario
- userdel
- Elimina una cuenta; -r borra su home
- userdel [-r] usuario
- usermod
- Modifica los atributos de una cuenta
- usermod [-g grupo] [-d home] [-s shell] usuario
- whereis
- Localiza binario, fuentes y manual
- whereis comando
- which
- Muestra la ruta completa de un ejecutable
- which comando
- Fuente: Guía de referencia de comandos Linux; Wiki de GUTL, «Más de 400 comandos para GNU/Linux».
- 40

## Diapositiva 41

- Comandos Linux · archivos, directorios, usuarios y grupos
- Ing. Angelmiro Quiroz Parra
- aparra19@udi.edu.co
