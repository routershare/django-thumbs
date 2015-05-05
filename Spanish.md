![http://media.django.es/djangothumbs.jpg](http://media.django.es/djangothumbs.jpg)
# django-thumbs #

### La forma más sencilla de crear miniaturas para imágenes con Django. Funciona con cualquier StorageBackend. ###

This page is also available in **[English](http://code.google.com/p/django-thumbs/)**

## Características ##

  * Fácil de integrar en el código (no hay cambios en la base de datos, funciona como un ImageField)
  * Funciona perfectamente con StorageBackend
  * Genera miniaturas después de que la imagen sea cargada en memoria
  * Elimina las miniaturas cuando se elimina el archivo de imagen
  * Fácil acceso a las URLs de las miniaturas (método similar al de ImageField)

## Instalar ##

  1. Descarga [thumbs.py](http://django-thumbs.googlecode.com/files/thumbs.py)
  1. Impórtalo en tu _models.py_ y reemplaza `ImageField` por `ImageWithThumbsField` en tus modelos
  1. Añade un atributo `sizes` con de una lista de tamaños que deseas para las miniaturas
  1. Asegúrate de que has definido `MEDIA_URL` en tu settings.py
  1. ¡Eso es todo!

## Ejemplo funcional ##

_models.py_
```
from django.db import models
from thumbs import ImageWithThumbsField

class Persona(models.Model):
    foto = ImageWithThumbsField(upload_to='imagenes', sizes=((125,125),(200,200)))
    otra_foto = ImageWithThumbsField(upload_to='imagenes')
```

En este ejemplo tenemos un modelo `Persona` con 2 campos imagen.

Puedes ver que el campo `otra_foto`no tiene el atributo `sizes`. Este campo funciona exactamente de la misma manera que un `ImageField` normal.

El campo `foto` tiene un atributo `sizes` que especifica el tamaño de las miniaturas deseadas. Este campo funciona de la misma manera que `ImageField` pero también crea las miniaturas especificadas al subir un nuevor archivo y las elimina cuando el archivo es eliminado.

Con `ImageField` se obtiene la URL de la imagen con: `alguien.photo.url` Con `ImageWithThumbsField` la imagen original se obtiene de la misma manera. También se obtiene la dirección URL de cada miniatura especificando su tamaño: En este ejemplo usamos `alguien.photo.url_125x125` y `alguien.photo.url_200x200` para obtener las URLs de ambas miniaturas.

## Desinstalar ##

En cualquier momento puedes echarte atrás y volver a usar `ImageField` de nuevo sin alterar la base de datos o cualquier otra cosa. Basta con sustituir `ImageWithThumbsField` por `ImageField` de nuevo y asegurarte de eliminar el atributo `sizes`. Todo funcionará de la misma forma que antes de usar django-thumbs. Sólo recuerda eliminar las miniaturas generadas en el caso de que no quieras seguir teniéndolas.