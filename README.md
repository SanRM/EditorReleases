Este repositorio contiene las versiones oficiales de **Editor Mágico**, el editor de vídeos automático. A continuación se detalla el funcionamiento del sistema de autoactualizaciones y el procedimiento para verificar manualmente la versión disponible, considerando que el servicio público de Electron implementa un mecanismo de caché que puede retrasar hasta 20 minutos la reflección de una nueva versión.

## 1. Caché del servicio de actualizaciones

* El endpoint `update.electronjs.org` almacena en su CDN la metainformación de la versión más reciente de Editor Mágico.
* Esta fuente consulta GitHub únicamente cada 15–20 minutos para actualizar su caché.
* Durante ese intervalo, todas las solicitudes al URL de actualización devolverán la misma versión almacenada en caché, aun cuando ya exista un nuevo tag o asset disponible en GitHub.

## 2. Verificación de la versión activa

Para determinar qué versión está sirviendo el servicio en un momento dado:

1. Sustituya `[plataforma]` y `[versión_actual]` en la siguiente URL:

   ```
   https://update.electronjs.org/SanRM/EditorReleases/[plataforma]/[versión_actual]
   ```
2. Abra la URL resultante en un navegador web.
3. El JSON de respuesta indicará la siguiente versión registrada, es decir, la versión mayor a la especificada en `[versión_actual]`.
4. Este mismo JSON es utilizado por `update-electron-app` para comprobar la disponibilidad de una actualización y para determinar desde dónde descargarla.

## 3. Recomendaciones de uso

* No es necesario iniciar la aplicación para conocer la versión activa; basta con consultar la URL en un navegador.
* Tras publicar un nuevo release en GitHub, aguarde aproximadamente 15 a 20 minutos antes de volver a consultar el endpoint, dado que el caché requiere ese tiempo para renovarse.

Con este procedimiento podrá comprender y verificar con exactitud el estado de las actualizaciones de Editor Mágico.
