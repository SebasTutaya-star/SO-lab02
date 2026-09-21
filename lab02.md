
# Laboratorio 02: Instalación de xv6 sobre Ubuntu (WSL)

**Estudiante:** Sebastian Tutaya  
**Curso:** Sistemas Operativos (IS-380) - UNSCH  

---

## 1. Ejecución de comandos en xv6 (Parte A)

Se arrancó el núcleo xv6 emulado mediante QEMU y se realizaron pruebas del sistema de archivos y llamadas al sistema con los comandos mostrados en la guia:

Arranque de xv6 y comandos de la Parte A

Comandos Realizados:
- "ls": Listado de archivos iniciales en xv6. 
- "echo Sebastian Tutaya": Salida estándar por consola.
- "mkdir SO-2026": Creación de directorio invocando la syscall "sys_mkdir".
- "ls": Verificación del nuevo directorio.
- "cat README": Lectura de archivo existente.
- "echo prueba de sistema de archivos > archivo.txt": Redirección y escritura mediante llamadas al sistema de archivos ("open", "write").
- "cat archivo.txt" y "wc archivo.txt": Lectura y conteo de líneas, palabras y bytes.

---

## 2. Inspección de llamadas al sistema (Parte C)

Se localizaron la interfaz y la implementación para "fork" y "read":

"""text
kernel/syscall.h:1:#define SYS_fork    1
kernel/sysproc.c:89:uint64 sys_fork(void)

kernel/syscall.h:5:#define SYS_read    5
kernel/sysfile.c:64:uint64 sys_read(void)

---

## 3. Pregunta de Reflexión (Parte D)

## ¿Qué diferencia se observa entre la interfaz de una llamada al sistema y su implementación interna?

- La Interfaz (kernel/syscall.h): Es el punto de contacto visible para el usuario. Se compone simplemente de un identificador numérico (por ejemplo, #define SYS_fork 1 o #define SYS_read 5). Define qué servicio se puede solicitar al sistema operativo, actua como un contrato fijo entre el programa y el núcleo.   

- La Implementación interna (kernel/sysproc.c, kernel/proc.c, kernel/sysfile.c): Es el código real que se ejecuta dentro del núcleo con privilegios de administrador del procesador. Define cómo se realiza el trabajo: aquí se asignan páginas de memoria física (uvmcopy()), se duplican tablas de procesos o se leen bloques directamente del disco.