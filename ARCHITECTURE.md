# Estructura de arquitectura

Este proyecto usa Clean Architecture dentro del módulo `:app`, con límites de paquetes para que el ejemplo siga siendo pequeño y visible. No añade módulos Gradle ni un framework de inyección.

```text
app/src/main/java/com/cuscatlan/myfirstbankingapp/
├── core/network/NetworkModule.kt
├── data/
│   ├── mapper/PokemonMappers.kt
│   ├── remote/PokeApi.kt
│   └── repository/PokemonRepositoryImpl.kt
├── domain/
│   ├── model/Pokemon.kt, PokemonDetail.kt
│   ├── repository/PokemonRepository.kt
│   └── usecase/GetPokemonListUseCase.kt, GetPokemonDetailUseCase.kt
├── presentation/
│   ├── home/HomeScreen.kt, PokemonListViewModel.kt, PokemonListUiState.kt
│   └── detail/PokemonDetailScreen.kt, PokemonDetailViewModel.kt, PokemonDetailUiState.kt
├── ui/theme/
└── MainActivity.kt
```

## Sentido de las dependencias

- `domain` declara los modelos, el contrato `PokemonRepository` y los casos de uso. No importa Android, Retrofit ni DTOs.
- `data` conoce `PokeApi`, traduce DTOs a modelos de dominio y proporciona `PokemonRepositoryImpl`.
- `presentation` depende de casos de uso y modelos de dominio. Los composables observan estado y emiten acciones.
- `MainActivity` actúa como composition root: crea las dependencias concretas y las pasa mediante factories. Para este ejemplo didáctico, la creación manual es suficiente.

## Recorrido de la lista

`HomeScreen` → `PokemonListViewModel` → `GetPokemonListUseCase` → `domain.repository.PokemonRepository` → `data.repository.PokemonRepositoryImpl` → `PokeApi` → DTO → mapper → modelo `Pokemon`.

El detalle sigue el mismo límite mediante `GetPokemonDetailUseCase` y `PokemonDetail`.

## Decisiones para clase

- Se mantienen paquetes dentro de un solo módulo Gradle para concentrarse en los límites de código. Extraer `:domain` o `:data` a módulos puede ser una evolución posterior, no un requisito de Clean Architecture.
- Hay casos de uso para las dos intenciones de producto que usan la capa de datos. La búsqueda simple permanece en el ViewModel, pues aquí solo transforma el estado presentado.
- `PokemonRepositoryImpl` coordina la fuente remota y el mapeo. Si se añade persistencia o caché, la política de fuentes puede evolucionar dentro de `data`.
- La app mantiene Compose, Navigation y Retrofit; solo cambia qué capa los conoce.
