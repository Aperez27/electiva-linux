# Instalación de Ubuntu Desktop 26.04 LTS

Guía de despliegue de «Resolute Raccoon»
Angelmiro Quiroz Parra — Ingeniero Informático (UDI)

## Contenido

- Novedades de la versión 26.04 LTS
- Requisitos de hardware y compatibilidad
- Preparación del medio de instalación
- Mitigación de conflictos previos
- Proceso de instalación y particionado
- Pasos posteriores y resolución de problemas

---

## NOVEDADES — Qué cambia en «Resolute Raccoon»

### Pilares de la versión

- **Soporte largo (5 años):** mantenimiento de seguridad extensible hasta 15 años con suscripción profesional.
- **Pila renovada (Kernel 7.0.0-14):** entorno de escritorio GNOME 50.1 sobre Wayland por defecto.
- **Seguridad e IA (Local):** computación confidencial e integración de inteligencia artificial sin envío de datos.

---

## REQUISITOS — Hardware, medio de instalación e integridad

### Requisitos de hardware

| Componente     | Mínimo                     | Recomendado                   |
|----------------|----------------------------|-------------------------------|
| Procesador     | 64 bits, dual-core 2,0 GHz | Quad-core 2,5 GHz o superior  |
| Memoria RAM    | 6 GB                       | 8 GB o más                    |
| Almacenamiento | 25 GB en SSD               | 100 GB en NVMe                |
| Gráficos       | 1024 × 768                 | 1920 × 1080 con aceleración   |

> Con menos de 4 GB de RAM se recomienda desplegar sabores ligeros: Xubuntu o Lubuntu.

### Descarga y verificación de la imagen

- ISO oficial de 5,9 GB desde ubuntu.com
- Validación obligatoria del checksum SHA256
- La integridad del medio evita fallos de segmentación

Windows (PowerShell):

    Get-FileHash ubuntu-26.04-desktop-amd64.iso -Algorithm SHA256

Linux y macOS (Terminal):

    sha256sum ubuntu-26.04-desktop-amd64.iso

### Medio booteable con Rufus

Configuración estricta para el estándar UEFI:

- Esquema de partición GPT
- Sistema de destino UEFI (non CSM)
- Sistema de archivos FAT32 para la partición ESP
- Modo de escritura: imagen ISO

Alternativas: balenaEtcher en macOS y Windows, Impression en Linux.

### Mitigación de conflictos

- **Intel RST (conmutar a AHCI):** con RAID activo el instalador no detecta las unidades. Windows exige reconfiguración previa para evitar el error INACCESSIBLE_BOOT_DEVICE.
- **BitLocker (clave obligatoria):** en arranque dual, tener a mano la clave de recuperación de la cuenta Microsoft antes de iniciar el instalador.
- **Inicio rápido (usar «Reiniciar»):** el apagado híbrido deja las particiones NTFS en hibernación bloqueada.

### Acceso a BIOS y menú de arranque

| Fabricante | Acceso BIOS/UEFI | Menú de arranque |
|------------|------------------|------------------|
| Lenovo     | F2 · Fn+F2       | F12              |
| HP         | F10              | F9               |
| Dell       | F2               | F12              |
| ASUS       | F2 · Supr        | F8               |

En equipos Apple se mantiene pulsada la tecla Opción durante el encendido y se selecciona el volumen «EFI Boot».

---

## INSTALACIÓN — El recorrido del instalador, pantalla por pantalla

### Idioma, teclado y red

El instalador de la 26.04 está construido sobre Flutter.

- El idioma define los locales del sistema y la terminal
- Ajustes de accesibilidad disponibles desde el inicio
- La red permite descargar microcódigo de CPU y controladores privativos
- Opción de probar el sistema antes de instalarlo

### Selección de software

- **Predeterminada:** navegador y utilidades base, para equipos que se personalizan desde cero
- **Ampliada:** incluye LibreOffice 26.8 y la suite multimedia
- **Software de terceros:** activar siempre, para drivers NVIDIA y códecs

### Configuración de disco

- **Borrado e instalación limpia:** habilita LVM y cifrado de disco con TPM
- **Junto a Windows:** deslizador de espacio y gestión del arranque con GRUB
- **Particionado manual:** control granular para usuarios avanzados

### Esquema recomendado para 100 GB

| Punto de montaje | Tamaño   | Formato | Función                        |
|------------------|----------|---------|--------------------------------|
| /boot/efi        | 512 MB   | FAT32   | Partición de sistema EFI       |
| / (raíz)         | 40 GB    | EXT4    | Sistema operativo y binarios   |
| /home            | Restante | EXT4    | Datos de usuario               |
| swap             | 4 GB     | Swap    | Área de intercambio de memoria |

> Lógica de swap: con RAM menor a 4 GB, swap igual a la RAM; con más de 8 GB, el 50 % de la RAM.

### Despliegue en VirtualBox 7.2

- Instalación desatendida para despliegues ágiles
- Máquina con 8 GB de RAM y 4 vCPU
- Tiempo estimado de 10 a 15 minutos

> El método desatendido deja el sistema en inglés: en Settings > Region & Language
> se instala el paquete de español y se ajusta el teclado a «Spanish Windows».

### Optimización tras el primer reinicio

- Actualización de repositorios y limpieza de paquetes obsoletos
- Sincronización del reloj en arranque dual, por el conflicto UTC frente a hora local
- Activación de drivers NVIDIA privativos en «Más controladores»
- Códecs multimedia y revisión de las opciones de privacidad de la IA local

```
sudo apt update && sudo apt upgrade -y && sudo apt autoremove
timedatectl set-local-rtc 1
sudo apt install ubuntu-restricted-extras
```

---

## PUESTA A PUNTO — Qué hacer después de instalar Ubuntu

### Actualización y códecs

Sistema al día: actualización de bases de datos de paquetes y parches de seguridad
recientes, desde la tienda de aplicaciones o la terminal.

```
sudo apt update && sudo apt upgrade -y
```

Códecs multimedia: por derechos de autor, Ubuntu no incluye ciertos formatos; el
paquete restringido habilita MP3, MP4 y las fuentes de Microsoft.

```
sudo apt install ubuntu-restricted-extras -y
```

### Controladores y seguridad básica

Controladores:
- Herramienta «Más controladores» en el menú de aplicaciones
- Opción «propietario, probado» en tarjetas Nvidia o AMD
- Drivers privativos de Wi-Fi y Bluetooth cuando la red se corta
- Reinicio del equipo tras aplicar los cambios

Seguridad:
- Activación del cortafuegos integrado
- Contraseña robusta de la cuenta de usuario
- Revisión de las actualizaciones automáticas

```
sudo ufw enable
```

### Aplicaciones, ajustes y respaldo

Esenciales (apt): navegador, reproductor VLC, control de versiones y utilidades de compresión.

```
sudo apt install vlc git gnome-tweaks unrar p7zip-full -y
```

Flatpak (dos tiendas): Ubuntu prioriza Snap; añadir Flathub amplía el catálogo disponible.

```
sudo apt install flatpak gnome-software-plugin-flatpak -y
```

Retoques y respaldo (Timeshift): GNOME Tweaks ajusta fuentes, botones de ventana y
porcentaje de batería. Timeshift guarda puntos de restauración del sistema.

### Puntos de restauración con Timeshift

Configuración inicial:
- Tipo de instantánea: RSYNC en discos EXT4 o BTRFS si el sistema usa ese formato
- Disco de destino distinto al del sistema, con espacio para varias instantáneas
- Programación diaria y semanal, con /home excluido por defecto

```
sudo apt install timeshift -y
sudo timeshift --create --comments "base limpia"
```

Uso y recuperación:
- Instantánea manual antes de cambiar kernel, drivers o repositorios
- Restauración desde la aplicación: seleccionar la fecha y confirmar
- Si el sistema no arranca, se restaura desde el USB en vivo con Timeshift instalado en la sesión

> No sustituye el respaldo de archivos personales: para eso, Déjà Dup o un disco externo.

### Resolución de problemas

| Síntoma                        | Causa y solución técnica |
|--------------------------------|--------------------------|
| El USB no es detectado         | Conflicto con Secure Boot o esquema MBR. Verificar que el USB sea GPT/UEFI. |
| Pantalla negra                 | Incompatibilidad del kernel con Wayland y NVIDIA. Pulsar «e» en GRUB y añadir nomodeset. |
| Cursor girando · bug de Mutter | Error del gestor de ventanas al conectar monitores en caliente. Se corrige en la 26.04.1 LTS. |
| Unidades no visibles           | El sistema está en modo RAID/RST. Cambiar a AHCI en la BIOS. |

> Ubuntu 26.04 utiliza Wayland por defecto bajo GNOME 50.1. Ante fallos persistentes con
> aplicaciones heredadas, conviene iniciar sesión seleccionando «Ubuntu on Xorg».
> — Nota final de la guía de instalación

---

Gracias — Facultad de Ingenierías · UDI — aparra19@udi.edu.co
