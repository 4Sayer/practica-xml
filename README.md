# Práctica XML y DTD

## Objetivo
Diseñar documentos XML y validarlos mediante DTD internos y externos, gestionando los artefactos con Git.

## Ejercicio 1: Pedido
### Modelo propuesto
Una jerarquía independiente para destinatario, artículo, dirección (dividida en calle e interior) y fecha de entrega.
### Decisiones de diseño
Se separaron los campos de la dirección y fecha en etiquetas distintas para permitir búsquedas exactas e independientes.

## Ejercicio 2: Nota
### DTD externo
Reglas importadas desde `nota.dtd`.
### DTD interno
Reglas contenidas en el bloque `<!DOCTYPE nota [ ... ]>`.
### Pruebas realizadas
Se validó que cambiar el orden o los nombres de las etiquetas hace que el archivo sea inválido.

## Ejercicio 3: Matrícula
### Modelo
Organización de la matrícula separando los datos personales del pago.
### Cardinalidad
Se implementó el símbolo `+` en `<domicilio>` para forzar la existencia de "al menos uno".
### Restricción del atributo tipo
Se usó `<!ATTLIST domicilio tipo (familiar|habitual) #REQUIRED>` para hacer obligatorio el atributo y limitar sus opciones.
### DTD externo
Validación modular mediante el archivo independiente `matricula.dtd`.
### DTD interno
Las mismas reglas incrustadas localmente en `matricula-interno.xml`.
### Pruebas realizadas
Confirmación de fallos al intentar remover el atributo obligatorio o cambiar su valor por uno ajeno a la enumeración.

## Conclusiones
1. Un XML bien formado cumple la sintaxis de etiquetas; uno válido además obedece el DTD.
2. El DTD asegura la integridad de la estructura de datos.
3. El DTD externo se reutiliza entre archivos; el interno es solo para un documento aislado.
4. La cardinalidad se expresa con `?`, `*`, y `+`.
5. Se restringe con una lista en el `ATTLIST` (ej: `(opcion1|opcion2)`).
6. Git permitió realizar cambios y experimentar sin riesgo a perder el trabajo previo.
7. `git diff` mostró exactamente qué líneas cambiaron; `git restore` deshizo los errores en las pruebas negativas.
8. Crear la rama `dtd-interno-matricula` permitió trabajar en el DTD interno sin corromper la versión externa aprobada.
