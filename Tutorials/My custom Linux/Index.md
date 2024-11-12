# Cómo instalar Linux Debian (y configurarlo como yo)

## Pre-requisitos
- Saber leer (obligatorio).
- Conexión a Internet (obligatorio).
- Copia de seguridad de todos los archivos importantes (recomendado).
- Pendrive de al menos 8 GB, vacío.

## Requisitos del sistema
- Computadora, ya sea con Linux o con Windows. Este tutorial es para gente que viene de Windows.
- 8 GB de RAM (recomendado), 2 GB de RAM (mínimo)
- 20 GB de espacio en disco (en realidad se usa menos, pero digo una cantidad grande por si acaso)
- Procesador de 2 núcleos a 1.6 GHz (Intel Core 2 Duo o AMD Athlon equivalente).

## Procedimiento

1. Andá a la [página de descargas de Linux Debian](https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/) y seleccioná la que diga **debian-live-x.x.x-amd64-gnome.iso** (x.x.x es la versión, que puede variar).

2. [Descargá Rufus](https://github.com/pbatard/rufus/releases/download/v4.4/rufus-4.4p.exe) y abrilo.

3. Conectá un pendrive de al menos 8GB.

4. Selecciona el pendrive en Rufus.

5. Seleccioná la ISO que descargaste recién.

6. Click en Grabar (START o INICIAR), esperás a que termine.

7. Presionás `win + R`

8. Copiás y pegás este comando: `shutdown /r /fw /t 0` para reiniciar a la BIOS.

9. Moviendote con las flechas vas al sector de orden de arranque y seleccionas para que inicie desde el pendrive.

10. Guardar y reiniciar.

11. Seguis las instrucciones de instalación que te va a decir ahí.

12. Una vez instalado, abrí una terminal y poné este comando:

```help```