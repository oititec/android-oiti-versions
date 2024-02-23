# Changelog

#### 6.0.1

**Data: 23/02/2024**

- Correção `KoinJavaComponent.inject<Context>(Context::class.java)` gerando crashs no SDK ao iniciar fluxo de documentoscopia.
- Correção para plataformas hibridas em alguns casos não eram aplicadas as customizações de cores

#### 6.0.0

**Data: 22/01/2024**

- Parâmetro `PARAM_ENDPOINT` removido, usar o `PARAM_ENVIRONMENT`.
- Nova forma de customização das cores e fontes para plataformas hibridas, caso o `PARAM_HYBRID` seja true.
- Implementação do Koin para injeção de dependências.
- Nova tela de instruçoes.
- Adicionado Device Inlligence
- Adicionado Device Behavior
- Adicionado Device Location
- Adicionado Device Info

- **Guia de migração com breaking changes da versão** [6.0.0](https://github.com/oititec/android-oiti-versions/blob/master/Liveness2D/BreakingChange/Migration-Guide-6.0.0.md)

**Necessário incluir a PERMISSÃO de LOCALIZAÇÃO:**
Seguir as instruções de permissões disponíveis [neste link.](https://devcenter.certiface.io/docs/guia-de-instalacao-android#passo-3-permiss%C3%A3o-de-localiza%C3%A7%C3%A3o)

#### 5.8.0

Data: 29/08/2023

- Novo parâmetro adicionado `PARAM_ENVIRONMENT` que recebe um objeto do tipo `Environment.HML` por default.
- Com a adição do `PARAM_ENVIRONMENT` o `PARAM_ENDPOINT` foi depreciado e movido para o novo parâmetro de environment.
- Nova forma de customização das cores adicionada para plataformas hibridas, caso o `PARAM_HYBRID` seja true.

```kotlin
val DocTheme = DocCopyTheme.Builder()
        .setBackgroundDismissColorHybrid("#73997d")
        .setBackgroundOkColorHybrid("#3b3bd4")
        .setTryAgainColorHybrid("#383531")
        .setBackgroundCameraColorHybrid("#70856e")
        .build()
```

#### 5.7.0

Data: 01/08/2023

- Implementado caminho para integrar com certiface api, adicionado 2 novos parametros para documentoscopia sendo eles o PARAM_CERTIFACE_ENV e PARAM_TICKET.

#### 5.6.2

Data: 21/07/2023

- Corrigido crash que ocorria com o custom loading nas plataformas hibridas.

#### 5.6.1

Data: 18/07/2023

- Ajuste para que a ofuscação não tenha impacto negativo no fluxo.

#### 5.6.0

Data: 21/06/2023

- Implementado custom loadings:
- Ponto de melhoria para tecnologias hibridas.

#### 5.5.0

- Compatibilidade com tecnologias híbridas

#### 5.4.0

- Melhorias de UX
- Ajuste na captura do documento
- Melhorias na qualidade de envio da imagem

#### 5.3.0

- Melhorias de UX
- Ajustes de fluxo

#### 5.2.0

- Melhorias de UX
- Permitir customização completa da documentoscopia
- Ajustes de fluxo

#### 5.2.0

- Correção de bug ao iniciar a câmera no liveness 2D

#### 5.1.0

- Melhorias de UX.
- Ajustes no Fluxo da Documentoscopia.
- Remoção de fontes não mais utilizadas.

#### 2.3.1

- Melhoria na captura das fotos.

#### 2.3.0

- Fluxo de recaptura de documento em caso de falha.

#### 2.2.1

- Ajuste na qualidade das imagens do Liveness.

#### 2.2.0

- [Documentoscopia com view customizável.](Documentscopy-CustomView.md)

#### 2.1.0

- [Documentoscopia.](Documentscopy-Usage.md)

#### [2.0.0](Migration-Guide-2.0.0.md)

- Layout redesenhado.
- Mecanismo de view customizável.

#### 1.6.1

- Adição do retorno `FaceCaptchaActivity.PARAM_RESULT_COD_ID`, com o código retornado na validação dos desafios.
- A partir desta versão, a chave `FaceCaptchaActivity.PARAM_RESULT_HASH` está obsoleta, e não retornará valor nenhum.

#### 1.6.0

- Otimização do uso de memória durante a captura de fotos.

#### [1.5.0](Migration-Guide-1.5.0.md)

- Refatoração do mecanismo de callbacks da camera2 api.
- Adição de dois códigos de erro: `ERROR_CAMERA_SETUP` e `ERROR_CAPTURE_PICTURE`.

#### [1.4.1](Migration-Guide-1.4.1.md)

- Adição de um helper para debug, que exibe logs na tela através de Toasts.

#### [1.4.0](Migration-Guide-1.4.0.md)

- Foi criado um novo enum, `FaceCaptchaErrorCode`, que indica o tipo de erro retornado pelo SDK.
- A chave `PARAM_RESULT_ERROR_APPKEY`, que indicava que a AppKey fornecida era inválida, ficou obsoleta nesta versão. Este erro agora pode ser verificado pelo código de erro `FaceCaptchaErrorCode.INVALID_APP_KEY `, através da chave `PARAM_RESULT_ERROR_CODE`.

#### 1.3.2

- Correção de crash relacionado a lateinit vars.

#### 1.3.0

- Melhoria no mecanismo de buffer de fotos da camera2 api.

#### 1.2.0

- Tratamento para erro OutOfMemory
- Verificação se aparelho está em chamada telefônica antes de iniciar os desafios.
