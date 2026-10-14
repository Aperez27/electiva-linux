# Configuracion-post-instalacion-Ubuntu

## Diapositiva 1

- GUÍA TÉCNICA
- Configuración post-instalación de Ubuntu 26.04 LTS
- Puesta a punto paso a paso desde la terminal
- Angelmiro Quiroz Parra Ingeniero Informático
- 1

## Diapositiva 2

- CONTENIDO
- Seis etapas de configuración
- Sincronización de repositorios y del sistema
- Soporte lingüístico y localización
- Códecs multimedia y controladores de hardware
- Software multifuente: Snap, Flatpak y AppImage
- Endurecimiento: sudo y cortafuegos
- Respaldo y resolución de problemas
- 2

## Diapositiva 3

- ETAPA 1
- Sincronización de repositorios y del sistema
- Prerrequisito obligatorio antes de cualquier otra configuración
- 3

## Diapositiva 4

- Actualizar el sistema
- Paso 1
- sudo apt update
- sudo ejecuta la orden con privilegios de administrador; apt update descarga los índices de los repositorios para conocer las versiones más recientes. No instala nada todavía.
- Paso 2
- sudo apt upgrade
- apt upgrade instala las versiones nuevas de los paquetes pendientes, incluidos los parches de seguridad de Canonical. Se confirma con Enter o con la tecla S.
- 4

## Diapositiva 5

- Encadenar, limpiar y ajustar el reloj
- Paso 3
- sudo apt update && sudo apt upgrade -y && sudo apt autoremove
- && ejecuta la orden siguiente solo si la anterior terminó sin error; -y responde «sí» automáticamente; autoremove elimina paquetes obsoletos y dependencias huérfanas.
- Arranque dual
- timedatectl set-local-rtc 1
- Hace que Ubuntu lea el reloj del hardware en hora local, como Windows, y corrige el desfase horario entre ambos sistemas (UTC frente a hora local).
- Fuente: documentación oficial de Ubuntu Desktop, Canonical, 2026.
- 5

## Diapositiva 6

- Omitir la sincronización inicial genera deuda técnica inmediata: la diferencia entre los metadatos locales y los servidores remotos deriva en conflictos de dependencias.
- Guía de puesta a punto profesional · Ubuntu 26.04 LTS
- 6

## Diapositiva 7

- ETAPA 2
- Soporte lingüístico y localización
- Idioma, corrección ortográfica y formatos regionales de fecha y moneda
- 7

## Diapositiva 8

- Completar el soporte de idiomas
- Procedimiento gráfico: no requiere comandos
- Abrir la utilidad Soporte de idiomas desde el menú
- Dejar que el sistema compruebe los componentes faltantes
- Descargar e instalar los paquetes sugeridos
- Pulsar «Aplicar a todo el sistema» para que el idioma llegue también a la pantalla de inicio de sesión
- Una instalación incompleta deja una interfaz híbrida y provoca errores en scripts que dependen de formatos de fecha o moneda.
- 8

## Diapositiva 9

- ETAPA 3
- Códecs multimedia y controladores de hardware
- Componentes privativos que no vienen en la instalación base por restricciones de licencia
- 9

## Diapositiva 10

- Instalar los códecs multimedia
- sudo apt install ubuntu-restricted-extras
- apt install descarga e instala el metapaquete ubuntu-restricted-extras , que agrupa códecs de audio y vídeo (H.264, MP3) y fuentes tipográficas estándar para documentos.
- Pide la contraseña de administrador y confirmación con Enter
- Durante la instalación se aceptan los términos de licencia de las fuentes de Microsoft
- Si se marcó «software de terceros» al instalar Ubuntu, solo completa las librerías que falten
- 10

## Diapositiva 11

- Gestionar controladores desde la terminal
- Ubuntu 26.04 retiró la pestaña gráfica «Controladores adicionales»
- Listar
- sudo ubuntu-drivers devices
- Detecta el hardware (GPU, Wi-Fi) y muestra los controladores certificados disponibles, marcando el recomendado.
- Instalar
- sudo ubuntu-drivers install [nombre_del_driver]
- Instala el controlador elegido. Se sustituye [nombre_del_driver] por el nombre exacto que arrojó el comando anterior.
- 11

## Diapositiva 12

- ETAPA 4
- Software multifuente: Snap, Flatpak y AppImage
- Varios formatos de paquete administrados desde una sola tienda
- 12

## Diapositiva 13

- Tres piezas del ecosistema
- GNOME Software
- Tienda
- Reúne paquetes .deb, Snaps y Flatpaks en una sola interfaz gráfica.
- Flatpak
- Aislado
- Aplicaciones aisladas y actualizadas desde el catálogo de Flathub.
- AppImage
- Portable
- Un único archivo ejecutable que no requiere instalación tradicional.
- 13

## Diapositiva 14

- Instalar la tienda y Flatpak
- Paso 1
- sudo apt install gnome-software \
- gnome-software-plugin-snap gnome-software-plugin-flatpak
- Instala GNOME Software y sus plugins para mostrar Snaps y Flatpaks en la tienda. La barra \ solo continúa la orden en la línea siguiente.
- Paso 2
- sudo apt install flatpak
- Instala el motor de ejecución Flatpak, necesario para descargar y correr aplicaciones en ese formato.
- 14

## Diapositiva 15

- Añadir Flathub y reiniciar
- Paso 3
- flatpak remote-add --if-not-exists flathub \
- https://dl.flathub.org/repo/flathub.flatpakrepo
- remote-add registra Flathub como fuente de aplicaciones; --if-not-exists evita un error si el repositorio ya estaba añadido.
- Obligatorio
- sudo reboot
- Reinicia el equipo para cargar las variables de entorno y que las aplicaciones Flatpak aparezcan en la tienda.
- 15

## Diapositiva 16

- Habilitar y ejecutar AppImage
- Paso 1
- sudo apt install libfuse2t64
- Instala la librería de compatibilidad FUSE que las AppImage necesitan para montarse y arrancar.
- Paso 2
- cd Descargas && chmod a+x archivo.AppImage
- cd entra en la carpeta de descarga; chmod a+x da permiso de ejecución a todos los usuarios.
- Paso 3
- ./archivo.AppImage
- ./ ejecuta el archivo de la carpeta actual. También sirve clic derecho › Ejecutar en el gestor de archivos.
- 16

## Diapositiva 17

- Instalar aplicaciones esenciales
- sudo apt install vlc git gnome-tweaks unrar p7zip-full -y
- Una sola orden apt install admite varios paquetes separados por espacios:
- vlc
- Reproductor multimedia compatible con casi cualquier formato
- git
- Sistema de control de versiones
- gnome-tweaks
- Retoques: fuentes, botones de ventana y porcentaje de batería
- unrar · p7zip-full
- Descompresión de archivos RAR y 7z
- Fuente: Hipertextual, «Qué hacer después de instalar Ubuntu».
- 17

## Diapositiva 18

- ETAPA 5
- Endurecimiento: sudo y cortafuegos
- Proteger credenciales y conexiones de red del equipo
- 18

## Diapositiva 19

- Quitar los asteriscos de sudo
- Ubuntu 26.04 muestra * al escribir la contraseña y así revela su longitud
- Paso 1
- sudo visudo
- Abre /etc/sudoers en modo seguro: valida la sintaxis antes de guardar.
- Paso 2
- Defaults !pwfeedback
- Línea que se añade al final del archivo; ! desactiva la opción pwfeedback.
- Paso 3
- Ctrl+O · Enter · Ctrl+X
- Atajos del editor nano: guardar, confirmar el nombre del archivo y salir.
- 19

## Diapositiva 20

- Nunca se edita /etc/sudoers con un editor convencional: un error de sintaxis puede bloquear el acceso administrativo al sistema.
- Advertencia de seguridad · usar siempre visudo
- 20

## Diapositiva 21

- Activar el cortafuegos
- Activar
- sudo ufw enable
- ufw (Uncomplicated Firewall) activa el cortafuegos integrado de Ubuntu; queda habilitado en cada arranque.
- Seguridad básica complementaria
- Contraseña robusta en la cuenta de usuario
- Revisión de las actualizaciones automáticas
- Fuente: Hipertextual, «Qué hacer después de instalar Ubuntu».
- 21

## Diapositiva 22

- ETAPA 6
- Respaldo y resolución de problemas
- Puntos de restauración y fallos frecuentes tras la instalación
- 22

## Diapositiva 23

- Crear un punto de restauración
- Paso 1
- sudo apt install timeshift -y
- Instala Timeshift , la herramienta que guarda instantáneas del sistema para volver a un estado anterior.
- Paso 2
- sudo timeshift --create --comments "base limpia"
- --create genera una instantánea inmediata; --comments le añade una etiqueta. Conviene crearla al terminar toda la puesta a punto.
- Fuente: Hipertextual, «Qué hacer después de instalar Ubuntu». Documentación de Timeshift.
- 23

## Diapositiva 24

- Configurar y recuperar con Timeshift
- Configuración inicial
- Instantánea RSYNC en discos EXT4; BTRFS si el sistema usa ese formato
- Disco de destino distinto al del sistema
- Programación diaria y semanal, con /home excluido
- Uso y recuperación
- Instantánea manual antes de cambiar kernel, drivers o repositorios
- Restauración desde la aplicación: fecha y confirmación
- Sin arranque: restaurar desde el USB en vivo
- No sustituye el respaldo de archivos personales: para eso, Déjà Dup o un disco externo.
- Fuente: Hipertextual, «Qué hacer después de instalar Ubuntu». Documentación de Timeshift.
- 24

## Diapositiva 25

- Paso 1
- Elegir el tipo de instantánea
- Abrir Timeshift desde el menú e introducir la contraseña de administrador
- En la pestaña Tipo, marcar RSYNC en discos EXT4
- Elegir BTRFS solo si el sistema se instaló en ese formato
- Captura: repositorio oficial de Timeshift en GitHub (licencia GPL).
- 25

## Diapositiva 26

- Paso 2
- Seleccionar el disco de destino
- En Ubicación , elegir una partición distinta a la del sistema
- Comprobar que haya espacio libre para varias instantáneas
- Un disco externo permite restaurar aunque el disco principal falle
- Captura: repositorio oficial de Timeshift en GitHub (licencia GPL).
- 26

## Diapositiva 27

- Paso 3
- Programar las instantáneas
- En Programación , activar los niveles Diario y Semanal
- Definir cuántas instantáneas se conservan por nivel (5 o menos ahorra espacio)
- En Usuarios , dejar /home excluido, como viene por defecto
- Captura: repositorio oficial de Timeshift en GitHub (licencia GPL).
- 27

## Diapositiva 28

- Paso 4
- Crear y restaurar una instantánea
- Crear : genera una instantánea manual y la añade a la lista.
- Restaurar : se elige la fecha, se revisa el resumen y se reinicia.
- Captura: repositorio oficial de Timeshift en GitHub (licencia GPL).
- 28

## Diapositiva 29

- Resolución de problemas
- Síntoma
- Causa y solución
- El USB no es detectado
- Conflicto con Secure Boot o esquema MBR: verificar que el USB sea GPT/UEFI
- Pantalla negra
- Incompatibilidad del kernel con Wayland y NVIDIA: pulsar «e» en GRUB y añadir nomodeset
- Cursor girando · bug de Mutter
- Error del gestor de ventanas al conectar monitores en caliente; corregido en la 26.04.1 LTS
- Unidades no visibles
- Sistema en modo RAID/RST: cambiar a AHCI en la BIOS
- Fuente: guía de instalación de Ubuntu Desktop 26.04 LTS.
- 29

## Diapositiva 30

- Ubuntu 26.04 utiliza Wayland por defecto bajo GNOME 50.1. Ante fallos persistentes con aplicaciones heredadas, conviene iniciar sesión seleccionando «Ubuntu on Xorg».
- Guía de instalación de Ubuntu Desktop 26.04 LTS
- 30

## Diapositiva 31

- Resumen de comandos · etapas 1 a 3
- Comando
- Función
- sudo apt update
- Actualiza los índices de repositorios
- sudo apt upgrade
- Instala las actualizaciones pendientes
- sudo apt autoremove
- Elimina paquetes obsoletos
- timedatectl set-local-rtc 1
- Reloj en hora local (arranque dual)
- sudo apt install ubuntu-restricted-extras
- Códecs y fuentes tipográficas
- sudo ubuntu-drivers devices
- Lista controladores disponibles
- sudo ubuntu-drivers install [driver]
- Instala el controlador elegido
- Fuente: elaboración propia con base en las guías de instalación y configuración de Ubuntu 26.04 LTS.
- 31

## Diapositiva 32

- Resumen de comandos · etapas 4 a 6
- Comando
- Función
- sudo apt install gnome-software …plugins
- Tienda con soporte Snap y Flatpak
- sudo apt install flatpak
- Motor de ejecución Flatpak
- flatpak remote-add … flathub
- Añade el repositorio Flathub
- sudo apt install libfuse2t64
- Compatibilidad con AppImage
- chmod a+x archivo.AppImage
- Permiso de ejecución
- sudo apt install vlc git gnome-tweaks …
- Aplicaciones esenciales
- sudo visudo
- Edición segura de sudoers
- sudo ufw enable
- Activa el cortafuegos
- sudo timeshift --create
- Crea un punto de restauración
- Fuente: elaboración propia con base en las guías de instalación y configuración de Ubuntu 26.04 LTS.
- 32

## Diapositiva 33

- Ing. Angelmiro Quiroz Parra · Facultad de Ingenierías
- aparra19@udi.edu.co
