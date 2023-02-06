## Instalação

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

No arquivo  `build.gradle` do módulo/app, adicione a dependência:

```gradle
dependencies {
    implementation 'br.com.oiti:liveness2d-sdk:5.3'
}
```
###  Changelog

- [Detalhes de versões](Liveness2D/Documentation/Changelog.MD)
