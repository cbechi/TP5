
**Alumno:** Carlos Bechi  
**Entorno sugerido:** Ubuntu
**Carpeta base de trabajo:** `~/tp_linux_practica`  
**Convenciones:** Bloques `bash` listan comandos ejecutables; 


---

## Ejercicios 

### 1. Listar todos los archivos del directorio `/bin`.
```bash
ls /bin
```

### 2. Listar todos los archivos del directorio `/tmp`.
```bash
ls /tmp
```

### 3. Listar todos los archivos de `/etc` que empiecen por `t` en orden inverso.
```bash
ls -1 /etc/t* | sort -r
```

### 4. Listar todos los archivos de `/dev` que empiecen por `tty` y tengan 5 caracteres.

```bash
ls /dev/tty??
```

### 5. Listar en `/dev` los que empiecen por `tty` y terminen en `1,2,3,4`.
```bash
ls /dev/tty*[1234]
```

### 6. Listar en `/dev` los que empiecen por `t` y acaben en `C1`.
```bash
ls /dev/t*C1
```

### 7. Listar todos los archivos, incluidos ocultos, del directorio raíz `/`.
```bash
ls -la /
```

### 8. Listar todos los archivos de `/etc` que **no** empiecen por `t`.
```bash
ls -1 /etc | grep -v '^t'
```

### 9. Listar todos los archivos de `/usr` y sus subdirectorios.
```bash
ls -R /usr
```

### 10. Cambiarse a `/tmp`, crear directorio `PRUEBA`.
```bash
cd /tmp
mkdir -p PRUEBA
```

### 11. Verificar que el directorio actual ha cambiado.
```bash
pwd
```

### 12. Mostrar el día y la hora actual.
```bash
date
```

### 13. Con un solo comando posicionarse en `$HOME`.
```bash
cd ~
```

### 14. Verificar que se está en `$HOME`.
```bash
pwd
```

### 15. Listar todos los ficheros de `$HOME` mostrando su número de inodo.
```bash
ls -lai ~
```

### 16. Borrar todos los archivos y directorios visibles de nuestro directorio `PRUEBA`.
```bash
rm -rf /tmp/PRUEBA/*
```

### 17. Crear estructura de directorios bajo `PRUEBA`.
```bash
mkdir -p /tmp/PRUEBA/{dir1/dir11,dir2,dir3/dir31/{dir311,dir312}}
tree /tmp/PRUEBA || find /tmp/PRUEBA -maxdepth 3 -print
```

### 18. Copiar `/etc/motd` a `mensaje` en `PRUEBA`.
```bash
cp /etc/motd /tmp/PRUEBA/mensaje 2>/dev/null ||   printf "Mensaje del día (placeholder)
" > /tmp/PRUEBA/mensaje
```

### 19. Copiar `mensaje` en `dir1`, `dir2`, `dir3`.
```bash
cp /tmp/PRUEBA/mensaje /tmp/PRUEBA/{dir1,dir2,dir3}/
```

### 20. Comprobar lo anterior con un solo comando.
```bash
ls -l /tmp/PRUEBA/{dir1,dir2,dir3}/mensaje
```

### 21. Copiar los archivos del directorio `rc.d` dentro de `/etc` a `dir31`.
```bash
cp -r "$src"/* /tmp/PRUEBA/dir3/dir31/ 2>/dev/null
```

### 22. Copiar en `dir311` los archivos de `/bin` con 4 letras y segunda letra `a`.
```bash
cp /bin/?a?? /tmp/PRUEBA/dir3/dir31/dir311/ 2>/dev/null
```

### 23. Copiar el directorio de otro usuario y sus subdirectorios debajo de `dir11`.
```bash
sudo cp -r /home/cbechi /tmp/PRUEBA/dir1/dir11/ 2>/dev/null
```

### 24. Mover `dir31` bajo `dir2`.
```bash
mv /tmp/PRUEBA/dir3/dir31 /tmp/PRUEBA/dir2/
```

### 25. Mostrar por pantalla los archivos ordinarios de `$HOME` y subdirectorios.
```bash
find ~ -type f -print
```

### 26. Ocultar el archivo `mensaje` de `dir3`.
```bash
mv /tmp/PRUEBA/dir3/mensaje /tmp/PRUEBA/dir3/.mensaje
```

### 27. Borrar los archivos y directorios de `dir1`, incluido el propio directorio.
```bash
sudo rm -rf /tmp/PRUEBA/dir1
```

### 28. Copiar a `dir312` los ficheros de `/dev` que empiecen por `t`, terminen en `[a-b]` y tengan 5 letras.
```bash
cp /dev/t???[ab] /tmp/PRUEBA/dir2/dir31/dir312/ 2>/dev/null
```

### 29. Borrar de `dir312` los que **no** acaben en `b` y tengan `q` como 4ª letra.
```bash
find /tmp/PRUEBA/dir2/dir31/dir312 -type f -name '???q?*' ! -name '*b' -delete
```

### 30. Mover `dir312` debajo de `dir3`.
```bash
mv /tmp/PRUEBA/dir2/dir31/dir312 /tmp/PRUEBA/dir3/
```

### 31. Enlace simbólico a `dir1` dentro de `dir3` llamado `enlacedir1`.
```bash
ln -s /tmp/PRUEBA/dir1 /tmp/PRUEBA/dir3/enlacedir1
```

### 32. Posicionarse en `dir3` y crear `nuevo1` dentro de `dir1` usando el enlace.
```bash
cd /tmp/PRUEBA/dir3
mkdir -p enlacedir1/nuevo1
```

### 33. Copiar los archivos que empiecen por `u` de `/bin` a `nuevo1`.
```bash
cp /bin/u* enlacedir1/nuevo1/ 2>/dev/null
```

### 34. Crear dos enlaces **duros** de `fich1` llamados `enlace` en `dir1` y `dir2`.
```bash
printf "contenido" > /tmp/PRUEBA/fich1
ln /tmp/PRUEBA/fich1 /tmp/PRUEBA/dir1/enlace 2>/dev/null || true
ln /tmp/PRUEBA/fich1 /tmp/PRUEBA/dir2/enlace
```

### 35. Borrar `fich1` y copiar `enlace` en `dir3`.
```bash
rm -f /tmp/PRUEBA/fich1
cp /tmp/PRUEBA/dir2/enlace /tmp/PRUEBA/dir3/
```

### 36. Enlace simbólico `enlafich1` al fichero `enlace` de `dir2` en `dir1`.
```bash
ln -s /tmp/PRUEBA/dir2/enlace /tmp/PRUEBA/dir1/enlafich1
```

### 37. Desde `dir1`, copiar (mediante el enlace) el archivo `fich1` dentro de `dir311`.
```bash
cd /tmp/PRUEBA/dir1
cp enlafich1 /tmp/PRUEBA/dir2/dir31/dir311/
```

### 38. Seguir en `dir1` y mostrar por pantalla las líneas de `fich1` usando el enlace.
```bash
cd /tmp/PRUEBA/dir1
cat enlafich1
```

### 39. Borrar `fich1` de `dir2`.
```bash
rm -f /tmp/PRUEBA/dir2/enlace
```

### 40. Borrar todos los archivos y directorios creados durante los ejercicios.
```bash
rm -rf /tmp/PRUEBA
```

### 41. Crear `dir2` y `dir3` bajo `PRUEBA`. Ver permisos actuales de `dir2`.
```bash
mkdir -p /tmp/PRUEBA/{dir2,dir3}
ls -ld /tmp/PRUEBA/dir2
```

### 42. Quitar permisos de **escritura** a propietario, grupo y otros de `dir2` (notación simbólica).
```bash
chmod a-w /tmp/PRUEBA/dir2
ls -ld /tmp/PRUEBA/dir2
```

### 43. Quitar permiso de **lectura** de `dir2` al resto (otros) usando notación octal.
```bash
chmod o-r /tmp/PRUEBA/dir2
ls -ld /tmp/PRUEBA/dir2
```

### 44. Mostrar permisos actuales de `dir2`.
```bash
ls -ld /tmp/PRUEBA/dir2
```

### 45. Crear bajo `dir2` un directorio `dir2l`.
```bash
mkdir -p /tmp/PRUEBA/dir2/dir2l
```

### 46. Concederse permiso de escritura en `dir2` e intentar de nuevo.
```bash
chmod u+w /tmp/PRUEBA/dir2
mkdir -p /tmp/PRUEBA/dir2/dir2l
```

### 47. Valores por omisión asignados a los archivos (umask).
```bash
umask 
```

### 48. Cambiar al directorio `dir3` e imprimir su trayectoria completa.
```bash
cd /tmp/PRUEBA/dir3 && pwd
```

### 49. Ver permisos asignados previamente a `dir3`.
```bash
ls -ld /tmp/PRUEBA/dir3
```

### 50. Reiniciar el ordenador.
```bash
sudo reboot

### 51. Crear `dira`, `dirb`, `dirc`, `dird` bajo el directorio actual.
```bash
mkdir -p dira dirb dirc dird
```

### 52. Comprobar permisos de acceso de los directorios recién creados (umask).
```bash
ls -ld dira dirb dirc dird
```

### 53. Crear el fichero `uno`, quitarle permisos de lectura y comprobar. Intentar borrarlo.
```bash
: > uno
chmod a-r uno
ls -l uno
rm -f uno
```

### 54. Quitar todos los permisos de **paso** (ejecución) a `dir2` y otorgar los demás.
```bash
chmod a=rw /tmp/PRUEBA/dir2
ls -ld /tmp/PRUEBA/dir2
```

### 55. Crear en el directorio propio (permisos especificados).
```bash
# carpeta1
mkdir -p ~/carpeta1 && chmod 700 ~/carpeta1
: > ~/carpeta1/fich1 && chmod 666 ~/carpeta1/fich1
: > ~/carpeta1/fich2 && chmod 644 ~/carpeta1/fich2

# carpeta2
mkdir -p ~/carpeta2 && chmod 750 ~/carpeta2
: > ~/carpeta2/file1 && chmod 660 ~/carpeta2/file1
: > ~/carpeta2/file2 && chmod 640 ~/carpeta2/file2

ls -l ~/carpeta1 ~/carpeta1/* ~/carpeta2 ~/carpeta2/*
```

### 56. Desde otro usuario probar operaciones.
```bash
cd /home/usuario2/carpeta1 
ls -l
cat fich1
echo "nuevo" >> fich1   
cat fich2    
echo "otro" >> fich2 

```

### 57. Traza completa del directorio actual; crear `correo` y `fuentes`.
```bash
pwd
mkdir -p correo fuentes
```

### 58. En `fuentes`, crear `dir1`, `dir2`, `dir3`.
```bash
cd fuentes && mkdir -p dir1 dir2 dir3
```

### 59. Crear `menus` bajo `correo` sin moverse.
```bash
mkdir -p ../correo/menus
```

### 60. En `HOME`, borrar los directorios colgantes de `fuentes` que acaben en número distinto de 1.
```bash
cd ~
rm -rf ~/fuentes/dir[0,2-9] 2>/dev/null
```

### 61. Ver si existe `/dev/tty2` y su fecha.
```bash
[ -e /dev/tty2 ] && ls -l --full-time /dev/tty2 || echo "No existe /dev/tty2"
```

### 62. Ver permisos de archivos que empiecen por `tt` en `/dev`.
```bash
ls -l /dev/tt*
```

### 63. Lista de archivos ordinarios en `/usr/bin`.
```bash
find /usr/bin -maxdepth 1 -type f -ls
```

### 64. Lista de directorios que cuelgan de `/`.
```bash
find / -maxdepth 1 -type d -printf "%f
" 2>/dev/null
```

### 65. Lista de ficheros que pertenezcan a `root`.
```bash
sudo find / -xdev -user root -type f -print 2>/dev/null
```

### 66. Lista de ficheros `.h` de `/usr/include`.
```bash
find /usr/include -type f -name '*.h' -print
```

### 67. Ejecutar comandos `ls*` de `/bin` (con cuidado).
```bash
ls /bin/ls*
for f in /bin/ls*; do echo "== $f =="; "$f" --help 2>/dev/null | head -n 2 || echo "no --help"; done
```

### 68. Tipo de cada fichero del árbol propiedad de un usuario conocido.
```bash
USR="$USER"; sudo find / -xdev -user "$USR" -type f -print0 2>/dev/null | xargs -0 file
```

### 69. Directorio `uno` en `HOME` con permisos: u=wx, g=rx, o=— (350).
```bash
mkdir -p ~/uno && chmod 350 ~/uno
ls -ld ~/uno
```

### 70. `uno1` dentro de `uno` con u=rwx, g=—, o=w (702).
```bash
mkdir -p ~/uno/uno1 && chmod 702 ~/uno/uno1
ls -ld ~/uno/uno1
```

### 71. Copiar a `menus` ficheros propiedad de un usuario conocido que acaben en número.
```bash
USR="$USER"
find ~ -type f -user "$USR" -regex '.*[0-9]$' -exec cp -t ~/correo/menus {} +
```

### 72. Usuarios conectados y enviar mensaje a un terminal.
```bash
who

```

### 73. Crear un archivo de tamaño 0.
```bash
: > cero.txt && ls -l cero.txt
```

### 74. Visualizar `/etc/motd`.
```bash
cat /etc/motd 2>/dev/null || echo "motd no disponible"
```

### 75. Guardar (ordenado por hora) las líneas de `who` del usuario deseado en `persona`.
```bash
USR="$USER"; who | awk -v u="$USR" '$1==u' | sort -k4,4 > persona
```

### 76. `carpeta` en `PRUEBA`, quitar lectura. Buscar todos los directorios bajo `HOME` a `direc`.
```bash
mkdir -p /tmp/PRUEBA/carpeta && chmod a-r /tmp/PRUEBA/carpeta
find ~ -type d > direc 2>/dev/null
```

### 77. Repetir redirigiendo errores a `mal`.
```bash
find ~ -type d > direc 2> mal
```

### 78. Añadir a `direc` los ficheros ordinarios que cuelguen de `/etc`.
```bash
find /etc -type f >> direc 2>/dev/null
```

### 79. Añadir a `nuevalista` nombres en `PRUEBA` que contengan `ai`, errores a `malos`.
```bash
find /tmp/PRUEBA -name '*ai*' -print >> nuevalista 2>> malos
```

### 80. Mostrar solo el tiempo de `who`.
```bash
TIMEFORMAT=%R; time (who >/dev/null)
```

### 81. Procesos del usuario `root`.
```bash
ps -u root -f
```

### 82. `proceso` con procesos sin terminal.
```bash
ps -e -o pid,tty,cmd | awk '$2=="?"' > proceso
```

### 83. Añadir fecha actual y `pwd` a `proceso`.
```bash
{ date; pwd; } >> proceso
```

### 84. Usuarios conectados ordenados por número de procesos.
```bash
ps -e -o user= | sort | uniq -c | sort -nr
```

### 85. Estado completo de procesos.
```bash
ps -eF
```

### 86. Datos de procesos de la shell actual.
```bash
ps -o pid,ppid,pgid,tty,stat,time,cmd --ppid $$ -p $$
```

### 87. Cuántos usuarios registrados.
```bash
getent passwd | wc -l
```

### 88. Cuántos usuarios usan bash.
```bash
getent passwd | awk -F: '$7 ~ /bash$/' | wc -l
```

### 89. Cuántos usuarios conectados.
```bash
who | wc -l
```

### 90. Líneas de un archivo que empiecen por L/l.
```bash
grep -E '^[Ll]' archivo.txt
```

### 91. Contar esas líneas.
```bash
grep -E '^[Ll]' archivo.txt | wc -l
```

### 92. Nombres de usuario (primer campo).
```bash
getent passwd | cut -d: -f1
```

### 93. Usuario y shell utilizado (último campo).
```bash
getent passwd | awk -F: '{print $1, $NF}'
```

### 94. Cambiar fecha de modificación.
```bash
touch -m -t 202401011200 archivo.txt
```

### 95. Firma md5.
```bash
md5sum archivo.txt
```

### 96. Modificar y verificar cambio de firma.
```bash
echo "cambio" >> archivo.txt
md5sum archivo.txt
```

### 97. Ocupación de particiones.
```bash
df -h
```

### 98. Proceso que más CPU consume.
```bash
ps -eo pid,comm,%cpu --sort=-%cpu | head -n 5
```

### 99. ¿Está corriendo `bash`?
```bash
pgrep -a bash && echo "bash en ejecución" || echo "bash no encontrado"
```

### 100. ¿Cuántos procesos que empiecen por k están corriendo?
```bash
ps -eo comm | grep -E '^k' | wc -l
```


