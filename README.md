## Avance de la práctica — Firebase + Jetpack Compose

Implementación del codelab [Build an Android app with Firebase and Jetpack Compose](https://firebase.google.com/codelabs/build-android-app-with-firebase-compose) sobre la carpeta `v1/start`.

- **Autor:** Pablojg18
- **Fecha:** 10 de noviembre de 2026
- **Proyecto Firebase:** `compose-firebase-codelab-87f7f`
- **Paquete Android:** `com.example.makeitso`
- **Reporte de avance y hallazgos:** [Avance_Practica_Firebase_Codelab.docx](Avance_Practica_Firebase_Codelab.docx)

### Funciones implementadas

- **Authentication:** registro con correo/contraseña vinculado a la cuenta anónima (`linkAccount`), estado de sesión reactivo en Settings.
- **Cloud Firestore:** escucha en tiempo real de la colección `tasks` filtrada por `userId`, reflejada en la UI con `Flow` + Compose.
- **Performance Monitoring:** traces personalizados `linkAccount` y `fetchConfig`.
- **Remote Config:** parámetro `show_task_edit_button` para mostrar u ocultar la opción de edición de tareas.

### Cómo ejecutar

1. Crear un proyecto de Firebase con Google Analytics habilitado.
2. Registrar una app Android con el paquete `com.example.makeitso`.
3. Descargar `google-services.json` y colocarlo en `v1/start/app/google-services.json`.
4. En **Authentication**, habilitar **Correo electrónico/contraseña** y **Anónimo**.
5. Crear la base de datos de **Cloud Firestore** y aplicar estas reglas:

```txt
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /tasks/{document} {
      allow create: if request.auth != null;
      allow read, update, delete: if request.auth != null
        && resource.data.userId == request.auth.uid
        && request.data.userId == resource.data.userId;
    }
  }
}
```

6. En **Remote Config**, agregar el parámetro `show_task_edit_button` (Boolean, `true`) y publicarlo.
7. Abrir la carpeta `v1/start` en Android Studio y ejecutar la app.

> `google-services.json` y `local.properties` están excluidos del repositorio por seguridad y por ser específicos de cada equipo.

## Make it So

This is the source code for Make It So, a sample app that demonstrates how to use Firebase in an Android app. 

The first version of this app was built in 2022 and you can find it in the v1 folder - you will also find instructions to set up your Firebase project and links to articles, documentation and codelabs that guide you through the code. 

Version 2 of this app was built in 2025 and you can find it in the v2 folder - you will also find instructions to set up your Firebase project and connect it to the Make it So app. This version implements a new architecture, based on the latest recommendations outlined in the [Android Guide to App Architecture documentation](https://developer.android.com/topic/architecture). Similarly, the UI was developed in accordance with the best practices described in [Android's "Develop UI for Android" documentation](https://developer.android.com/develop/ui).

## Contact

Please navigate to the [discussions page](https://github.com/FirebaseExtended/make-it-so-android/discussions/) if you have any questions or want to suggest changes to the Make it So app.
