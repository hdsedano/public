# 0. Instalar aplicaciones:
- Testdisk:
```
  sudo apt update
  sudo apt install testdisk
```
Esto instala PhotoRec y TestDisk en distribuciones basadas en Debian/Ubuntu

# 1. Haz una imagen de la tarjeta antes de escribir con ddrescue:
```
sudo dd if=/dev/sda of=~/backup_sd.img bs=4M status=progress
```
#La imagen queda con permisos de lectura,creé una copia en el directorio Documents. 

# 2. Prueba con TestDisk para reconstruir la tabla de particiones en la imagen:
```
sudo testdisk ~/backup_sd.img
```
1. Selecciona Intel → Analyse → Quick Search.
2. Si encuentra una partición FAT32, usa P para listar archivos.
3. Write la tabla de particiones si los archivos se ven bien.
   #Aviso "Try to unformat a FAT filesystem (Y/N)" R/ Y
   Para tarjetas SD/microSD estándar: Elige [ 512 ] (es el valor más común en tarjetas de cámaras).

# ¿Cuándo elegir Y (Sí)?
✔ Si formateaste la tarjeta por error (pero no guardaste datos nuevos después).
✔ Si quieres recuperar la estructura de carpetas (no solo archivos sin nombres).
✔ Si PhotoRec no encontró suficientes archivos (esto es un intento adicional).

# 3. Ejecuta photorec en la imagen:
```
sudo photorec /home/hernan/Documents/backup_sd.img
```
**Configuración óptima paso a paso:**
1. Selecciona [ File Opt ]:
  - Desmarca todos los formatos (con s).
  - Marca solo los que necesitas (ej: jpeg, mp4, mov).
  - Presiona b para guardar.
2. Elige [ Search ] → Whole.
3. Selecciona [ Options ]:
  - Paranoid:	No (más archivos, menos precisión)
  - Keep corrupted:	No (evita basura)
  - Expert mode:	Yes + ajustar Min file size a 0 KB
  - Low memory:	No
4. Presiona Enter para iniciar el escaneo.
5. Guarda los archivos recuperados en otro disco (no en la misma tarjeta/imagen).

