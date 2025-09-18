# TP – 5 Linux: Comandos, Usuarios/Grupos y Permisos

**Alumno:** Carlos Bechi  
**Entorno:** Ubuntu (consola en Windows 11 PRO)
**Carpeta de trabajo:** `~/tp_linux`




## PARTE I — Comandos de Linux

### Actividad 1
**Crear `provincias.txt` y visualizar el contenido.**
```bash
printf "Salta
Jujuy
Córdoba
Santa Fe
" > provincias.txt
cat provincias.txt
```


### Actividad 2
**Añadir “Buenos Aires” y “Mendoza” al final.**
```bash
printf "Buenos Aires
Mendoza
" >> provincias.txt
cat provincias.txt
```


### Actividad 3
**Listar archivos de `/dev` que empiezan por `tty`.**
```bash
ls -l /dev/tty*

```

### Actividad 4
**Crear cuatro subdirectorios en un solo comando: `formacion`, `ventas`, `personal`, `clientes`.**
```bash
mkdir -p {formacion,ventas,personal,clientes}
ls -l
```

### Actividad 5
**Crear archivos dentro de `ventas` con cualquier contenido.**  
`julio.txt`, `agosto.txt`.
```bash
cd ventas
printf "reporte mayo
"  > mayo.txt
printf "reporte junio
" > junio.txt
printf "reporte julio
" > julio.txt
printf "reporte agosto
" > agosto.txt
ls -l
cd ..
```

### Actividad 6
**Copiar a `clientes` todos los archivos creados en `ventas`.**
```bash
cp ventas/* clientes/
ls -l clientes
```

### Actividad 7
**Borrar el directorio `ventas`.**
```bash
rm -r ventas
ls -l
```

### Actividad 8
**Renombrar `clientes` a `clientes_2022`.**
```bash
mv clientes clientes_2022
ls -l
```

---

## PARTE II — Usuarios/Grupos y Permisos

> Ejecutar con privilegios (p. ej., `sudo`) en un Linux real o en WSL.

### Actividad 1
**Crear los grupos `administradores` y `desarrolladores`. Ver GID.**
```bash
sudo addgroup administradores
sudo addgroup desarrolladores

getent group administradores desarrolladores

```

### Actividad 2
**Crear usuarios `web` y `app` con grupo primario = `desarrolladores` (único grupo).**
```bash
sudo adduser --ingroup desarrolladores --disabled-password --gecos "" web
sudo adduser --ingroup desarrolladores --disabled-password --gecos "" app

# Verificación
id web && groups web && getent passwd web
id app && groups app && getent passwd app
```
- `id` muestra UID/GID; `groups` los grupos; `getent passwd` muestra la línea de `/etc/passwd`.

### Actividad 3
**Loguearse como `web` y crear `administracion.txt` accesible solo por `web` (lectura/escritura).**
```bash
sudo -iu web
cd ~
printf "solo web puede leer y escribir
" > administracion.txt
chmod 600 administracion.txt
ls -l administracion.txt
exit
```
- `chmod 600` → propietario: `rw`, grupo/otros: `---`.

### Actividad 4
**Como `app`, crear `compartido` y los ficheros `archivo1.txt`, `archivo2.txt`, `archivo3.txt`.**
```bash
sudo -iu app
cd ~
mkdir -p compartido
printf "contenido 1
" > compartido/archivo1.txt
printf "contenido 2
" > compartido/archivo2.txt
printf "contenido 3
" > compartido/archivo3.txt
ls -l compartido
exit
```

### Actividad 5
**Cambiar el grupo propietario de `archivo2.txt` a `desarrolladores`.**
```bash
sudo chgrp desarrolladores /home/app/compartido/archivo2.txt
ls -l /home/app/compartido/archivo2.txt
```

### Actividad 6
**Eliminar el usuario `app` sin borrar su directorio personal y observar propiedad de `/home/app`.**
```bash
sudo userdel app     
ls -ld /home/app
stat /home/app
```

### Actividad 7 — Caso Steve (archivo *Lista_Precios* confidencial en `/home/Steve`)

**Medidas de seguridad:**
1. **Cuentas separadas + bloqueo de sesión**: no compartir sesiones, usar bloqueo automático.
2. **Permisos POSIX estrictos**:
   ```bash
   chmod 700 /home/Steve
   chmod 600 /home/Steve/Lista_Precios
   ls -l /home/Steve/Lista_Precios
   ```
3. **Cifrado del archivo** con GnuPG (protege ante admins/robo de disco):
   ```bash
   sudo apt update && sudo apt install -y gnupg
   gpg -c /home/Steve/Lista_Precios         
   shred -u /home/Steve/Lista_Precios        
   # Para leer: gpg -d /home/Steve/Lista_Precios.gpg > /home/Steve/Lista_Precios
   ```

**Identificaciones solicitadas por la consigna:**
- **Medidas**: permisos 700/600, bloqueo de sesión/cuentas separadas.
- **Usuarios afectados**: “grupo” y “otros” (no Steve).
- **Permisos a cambiar**: lectura/escritura/ejecución para grupo/otros (revocar).
- **Verificación**: `ls -l` sobre archivo y HOME; pruebas de acceso con otro usuario.

---


