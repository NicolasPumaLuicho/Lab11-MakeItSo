# Lab 11 - Firebase (Make It So)

Aplicación Android del Laboratorio 11 de Programación en Móviles (Tecsup). El proyecto base es **Make It So** y en este laboratorio se le agregó Firebase: autenticación, Cloud Firestore y Performance Monitoring.

## Funcionalidad

- Inicio de sesión anónimo automático al abrir la app.
- Vinculación de la cuenta anónima con correo y contraseña desde la pantalla de Settings.
- Tareas guardadas en Cloud Firestore y filtradas por el `userId` del usuario autenticado.
- Lista de tareas en tiempo real con Kotlin Flow y `collectAsStateWithLifecycle`.
- Trazas de rendimiento para las operaciones `linkAccount`, `saveTask` y `updateTask`.

## Configuración de Firebase

Proyecto: `lab11-makeitso-c30ec`. El archivo de configuración está en `start/app/google-services.json`.

- **Authentication:** proveedores Email/Password y Anonymous habilitados.
- **Cloud Firestore:** base de datos en modo producción (nam5), colección `tasks`.
- **Analytics:** habilitado al crear el proyecto.

Reglas de Firestore usadas:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow create: if request.auth != null;
      allow read, update, delete: if request.auth != null && resource.data.userId == request.auth.uid;
    }
  }
}
```

## Cómo ejecutar

1. Abrir la carpeta `start` en Android Studio.
2. Usar **JDK 17**: Gradle 8.0.2 no sincroniza con Java 21 o superior.
3. Sincronizar el proyecto y ejecutar en un emulador o dispositivo Android.

## Video y evidencias

- Video del funcionamiento: `ScreenRecording.mp4`
- Capturas de la consola de Firebase y de la app: carpeta `evidencias/`
- Informe del laboratorio: `GLAB-S11-BPAREJA-2026-01-PUMA-LUCHO-NICOLAS.pdf` (y su versión DOCX)

## Commits del avance

1. Configuración del proyecto Firebase y `google-services.json`.
2. Vinculación de la cuenta anónima con correo y contraseña.
3. Pantalla de Settings según el estado de autenticación.
4. Consulta de tareas por usuario en Cloud Firestore.
5. Informe, evidencias y video.
