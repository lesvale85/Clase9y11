# 📱 Pokémon Clean App (MyFirstBankingApp)

Aplicación móvil para Android desarrollada en **Kotlin** y **Jetpack Compose**, siguiendo los principios de **Clean Architecture** y **MVVM**. 
Permite explorar el mundo Pokémon, consultar detalles, gestionar favoritos, alternar vistas (normal/compacta) y navegar sin conexión a internet (*Offline-First*).

---

## 🚀 Características Principales

- **Arquitectura Limpia (Clean Architecture)**: Separación estricta de responsabilidades en capas (`domain`, `data`, `presentation`).
- **Modo sin conexión (*Offline-First*)**: Almacenamiento local mediante **Room** con persistencia de caché y datos iniciales (*seed data*) para funcionar sin red.
- **Inyección de Dependencias**: Gestionada con **Koin**.
- **Gestión de Preferencias**: Uso de **DataStore** para guardar el estado de la vista (compacta/normal).
- **Interfaz Reactiva**: 100% construida con **Jetpack Compose** y Material 3.
- **Consumo de Red**: Cliente HTTP con **Retrofit** y carga de imágenes asíncronas con **Coil**.

---

## 🛠️ Tecnologías y Librerías

- **Lenguaje**: Kotlin
- **UI**: Jetpack Compose, Material 3, Navigation Compose
- **Inyección de Dependencias**: Koin BOM (`io.insert-koin`)
- **Base de Datos y Caché**: Room, DataStore Preferences
- **Red / API**: Retrofit, Gson Converter, OkHttp Logging Interceptor
- **Imágenes**: Coil 3 (`coil-compose`, `coil-network-okhttp`)
- **Pruebas**: JUnit 4, Coroutines Test

---

## 📂 Estructura del Proyecto

app/src/main/java/com/cuscatlan/myfirstbankingapp/
│
├── MainActivity.kt
├── PokemonApplication.kt
│
├── core/
│   └── network/
│       └── NetworkModule.kt
│
├── data/                                        # Capa de datos (Remoto, Local/Room, Repositorios)
│   ├── database/
│   │   └── SearchValidator.kt                   
│   ├── local/                                   # DAOs, Entidades de Room y Base de Datos
│   │   ├── CachedPokemonDetail.kt
│   │   ├── FavoriteDao.kt
│   │   ├── FavoriteEntity.kt
│   │   ├── PokemonDao.kt
│   │   ├── PokemonDatabase.kt
│   │   ├── PokemonDetailDao.kt
│   │   ├── PokemonDetailEntity.kt
│   │   ├── PokemonEntity.kt
│   │   └── PokemonStatEntity.kt
│   ├── mapper/                                  # Mapeadores entre DTOs, Entidades y Modelos de Dominio
│   │   └── PokemonMappers.kt
│   ├── preferences/                             # DataStore y Preferencias de usuario
│   │   └── SettingsRepositoryImpl.kt
│   ├── remote/                                  # Interfaces de Retrofit (PokeApi) y DTOs
│   │   └── PokeApi.kt
│   └── repository/                              # Casos de uso (Lógica de negocio)
│       ├── FavoriteRepositoryImpl.kt
│       └── PokemonRepositoryImpl.kt
│
├── di/                                          # Conexiones a Red, Base de Datos, Repositorios
│   └── AppModule.kt
│
├── domain/                                      # Capa de Dominio (Modelos puramente de negocio, Repositorios abstractos, Casos de uso)
│   ├── model/                                   # Modelos de datos de negocio
│   │   ├── Pokemon.kt
│   │   └── PokemonDetail.kt
│   ├── repository/
│   │   ├── FavoriteRepository.kt
│   │   ├── PokemonRepository.kt
│   │   └── SettingRepository.kt
│   └── usecase/
│       ├── GetPokemonDetailUseCase.kt
│       ├── GetPokemonListUseCase.kt
│       └── ToggleFavoriteUseCase.kt
│
├── presentation/                                # Capa de Presentación (UI con Jetpack Compose y ViewModels)
│   ├── detail/                                  # Pantalla y ViewModel de Detalle del Pokémon
│   │   ├── PokemonDetailScreen.kt
│   │   ├── PokemonDetailUiState.kt
│   │   ├── PokemonDetailViewModel.kt
│   │   └── PokemonDetailViewModelFactory.kt
│   └── home/                                    # Pantalla principal y ViewModel de la Pokédex
│       ├── HomeScreen.kt
│       ├── PokemonListUiState.kt
│       ├── PokemonListViewModel.kt
│       └── PokemonListViewModelFactory.kt
│
└── ui/
    ├── components/                              # Módulos de Inyección de Dependencias (Koin)
    │   ├── AppTextField.kt
    │   └── PrimaryButton.kt
    └── theme/                                   # Tema, Colores y Componentes visuales reutilizables
        ├── Color.kt
        ├── Theme.kt
        └── Type.kt


app/src/test/java/com/cuscatlan/myfirstbankingapp/ (Pruebas Unitarias)
│
├── ExampleUnitTest.kt
├── PokemonCardScreenshotTest.kt
├── PokemonListUiStateTest.kt
├── PokemonMappersTest.kt
├── RefreshPokemonFailureTest.kt
├── RefreshPokemonUseCaseTest.kt
└── SearchValidatorTest.kt
