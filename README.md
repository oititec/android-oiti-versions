<p align="center">
 <img src="Liveness3D/Documentation/Images/OitiHeader.png"/>
</p>

## Instalação e Atualização

### Requisitos mínimos (Liveness 2D e 3D)

- ##### `Gradle 6.8+`
- ##### `Android minSDK 21+`
- ##### `Android targetSDK 33+`
- ##### `androidx.core:core-ktx:1.6.0+`
- ##### `androidx.appcompat:appcompat:1.6.1+`

### Liveness 2D

#### via Gradle

No arquivo `settings.gradle` do projeto, adicione o repositório:

```gradle
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        maven { url "https://raw.githubusercontent.com/oititec/android-oiti-versions/master" }
    }
}
```

No arquivo `build.gradle` do módulo/app, adicione a dependência:

```gradle
dependencies {
    implementation 'br.com.oiti:liveness2d-sdk:5.8.0'
}
```

### Changelog

- [Detalhes de versões](Liveness2D/Documentation/Changelog.MD)

### Liveness 3D

#### via Gradle

No arquivo `settings.gradle` do projeto, adicione o repositório:

```gradle
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        maven { url "https://raw.githubusercontent.com/oititec/android-oiti-versions/master" }
    }
}
```

No arquivo `build.gradle` do módulo/app, adicione a dependência:

```gradle
dependencies {
    implementation 'br.com.oiti:liveness3d-sdk:9.1.0'
}
```

### Changelog

- [Detalhes de versões](Liveness3D/Documentation/Changelog.MD)

### Guias de migração

- [8.0.0](https://github.com/oititec/liveness-android-sdk/blob/main/Documentation/Migration-Guide-8.0.0.md) - BREAKING CHANGE
- [9.0.0](https://github.com/oititec/liveness-android-sdk/blob/main/Documentation/Migration-Guide-9.0.0.md) - BREAKING CHANGE
