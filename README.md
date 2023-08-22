# Superheroes App - Settings Feature

La aplicación Superheroes App permite a los usuarios personalizar su experiencia a través de la función de configuración. Con esta actualización, he implementado un manejo de datos que se almacenan en memoria utilizando DataStore. Esto garantiza que las preferencias del usuario se conserven incluso después de cerrar y volver a abrir la aplicación.

## Características Implementadas

- Cambio de modo nocturno.
- Encendido y apagado del Bluetooth.
- Ajuste de volumen.
- Activación y desactivación de la vibración.

## Uso de DataStore

He utilizado la biblioteca `androidx.datastore` para almacenar las preferencias del usuario de manera eficiente. Aquí hay un resumen de cómo se utilizó DataStore en la aplicación:

- Almacenamiento de nivel de volumen.
- Control de Bluetooth.
- Control de vibración.
- Cambio de modo nocturno.

## Código Fuente

El código fuente de esta funcionalidad se encuentra en los siguientes archivos:

- `SettingsActivity.kt`: Aquí se implementa la lógica principal de la pantalla de configuración, incluyendo la interacción con DataStore.

- `activitysettings.xml`: El diseño de la pantalla de configuración.

## Uso de DataStore

```kotlin
implementation("androidx.datastore:datastore-preferences:1.0.0")
// Obtener el DataStore
val dataStore: DataStore<Preferences> by preferencesDataStore(name = "settings")

// Guardar un valor en DataStore
private suspend fun saveVolume(value: Int) {
    dataStore.edit { preferences ->
        preferences[intPreferencesKey(VOLUME_LVL)] = value
    }
}

// Leer valores desde DataStore
private fun getSettings(): Flow<SettingsModel?> {
    return dataStore.data.map { preferences ->
        SettingsModel(
            volume = preferences[intPreferencesKey(VOLUME_LVL)] ?: 50,
            bluetooth = preferences[booleanPreferencesKey(KEY_BLUETOOTH)] ?: true,
            darkMode = preferences[booleanPreferencesKey(KEY_DARK_MODE)] ?: false,
            vibration = preferences[booleanPreferencesKey(KEY_VIBRATION)] ?: true
        )
    }
}

