<p align="center">
 <img src="Images/OitiHeader.png"/>
</p>

# Changelog

### [Versão 9.0.0](https://github.com/oititec/android-oiti-versions/releases/tag/9.0.0)

Data: 04/10/2023

- Atualização do `PARAM_FONTS`
- Remoção do `PARAM_FONTS_NEW_API`
- Breaking changes e guia de migração para a [9.0.0](https://github.com/oititec/liveness-android-sdk/blob/main/Documentation/Migration-Guide-9.0.0.md) 

### [Versão 8.1.1](https://github.com/oititec/android-oiti-versions/releases/tag/8.1.1)

Data: 21/09/2023

- Atualização da FaceTec - versão 9.6.49
  - Adicionadas novas verificações de injeção de vídeo no lado do dispositivo e no servidor para mitigar ameaças de IA generativa.
  - Melhorias de desempenho em dispositivos de nível inferior e intermediário, levando a melhorias na taxa de sucesso.
  - Correções para melhorar a compatibilidade de vários dispositivos Samsung, Redmi e Xiaomi.
  - Numerosas correções de melhoria de estabilidade.
  - Mensagens de registro aprimoradas.

### [Versão 8.1.0](https://github.com/oititec/android-oiti-versions/releases/tag/8.1.0)

Data: 29/08/2023

- Nova forma para customizar as cores adicionada, permitindo a passagem de um hexadecimal String para o builder do Liveness3DTheme.

```kotlin
val liveness3DTheme = Liveness3DTheme.Builder()
                // Colors for hybrid
                .guidanceCustomizationBackgroundColors("#73997d")
                .feedbackCustomizationTextColor("#15d100")
                .build()
```

### [Versão 8.0.1](https://github.com/oititec/android-oiti-versions/releases/tag/8.0.1)

Data: 24/08/2023

- Atualização da FaceTec - versão 9.6.42
  - Adicionadas novas verificações de injeção de vídeo no lado do dispositivo e no servidor para mitigar ameaças de IA generativa.
  - Melhorias de desempenho em dispositivos de nível inferior e intermediário, levando a melhorias na taxa de sucesso.
  - Correções para melhorar a compatibilidade de vários dispositivos Samsung, Redmi e Xiaomi.
  - Numerosas correções de melhoria de estabilidade.

### [Versão 8.0.0](https://github.com/oititec/android-oiti-versions/releases/tag/8.0.0)

Data: 11/08/2023

- **Breaking changes**
  - Novo PARAM_FONTS adicionado para APIs abaixo do (API level 26)
  - Novo Param_FONTS_NEW_API adicionado
  - A estrutura do `Liveness3DTheme` teve algumas propriedades removidas, segue a lista:
    - `guidanceCustomizationHeaderFont`
    - `guidanceCustomizationSubtextFont`
    - `guidanceCustomizationButtonFont`
    - `guidanceCustomizationReadyScreenHeaderFont`
    - `guidanceCustomizationReadyScreenSubtextFont`
    - `guidanceCustomizationRetryScreenHeaderFont`
    - `guidanceCustomizationRetryScreenSubtextFont`
    - `resultScreenCustomizationMessageFont`
    - `feedbackCustomizationTextFont`
  - A customização das fontes agora é feita somente pelo dicionário de chave e referencia ou caminho da fonte, assim como é aplicado com os textos. `Liveness3DFontsKey`.

### [Versão 7.1.2](https://github.com/oititec/android-oiti-versions/releases/tag/7.1.2)

Data: 21/07/2023

- Corrigido crash que ocorria com o custom loading nas plataformas hibridas.

### [Versão 7.1.1](https://github.com/oititec/android-oiti-versions/releases/tag/7.1.1)

Data: 17/07/2023

- Ajuste na propriedade RESULT_SUCCESS_MESSAGE á qual não aplicava customização.
- Revisão na estrutura da customização dos textos.

### [Versão 7.1.0](https://github.com/oititec/android-oiti-versions/releases/tag/7.1.0)

Data: 07/07/2023

- Atualização da FaceTec - versão 9.6.36
  - A propriedade feedbackEyesStraightAhead foi descontinuada.
  - Adicionada nova checagem de injeção de video no dispositivo e servidor para mitigar a ameaça das IAs Generativas.
  - Melhorias de estabilide.

### [Versão 7.0.0](https://github.com/oititec/android-oiti-versions/releases/tag/7.0.0)

Data: 21/06/2023

- Implementado custom loadings:
- Ponto de melhoria para tecnologias hibridas.

### [Versão 6.9.2](https://github.com/oititec/android-oiti-versions/releases/tag/6.9.2)

Data: 20/06/2023

- Ponto de correção encontrado com Koin:
- Ajuste na configuração do Koin para garantir inicialização e independência em apps que já possuem Koin ou não utilizam o framework.

### [Versão 6.9.1](https://github.com/oititec/android-oiti-versions/releases/tag/6.9.1)

Data: 15/06/2023

- Ponto de correção encontrado com Koin:
- Encontrado ponto onde dentro do application, android:name conflitava com o .App do manifest do SDK e não permitia o build do app.

### [Versão 6.9](https://github.com/oititec/android-oiti-versions/releases/tag/6.9)

Data: 30/05/2023

- Atualização do SDK para 6.9 trazendo melhorias de arquitetura interna
  - adicionado a possibilidade de customizar o campo resultScreenOverrideSuccessMessage que altera a mensagem de sucesso.
  - Atualizado modulo de uso interno para nova arquitetura
  - Várias correções de melhoria de estabilidade.

### [Versão 6.8](https://github.com/oititec/android-oiti-versions/releases/tag/6.8)

Data: 26/05/2023

- Atualização para Facetec v9.6.30
  - Adicionadas novas verificações de injeção de vídeo no lado do dispositivo e no lado do servidor para mitigar ameaças de IA generativas.
  - Melhorias de desempenho em dispositivos de nível baixo e intermediário, levando a melhorias na taxa de sucesso.
  - Correções para melhorar a compatibilidade de vários dispositivos Samsung e Redmi.
  - Várias correções de melhoria de estabilidade.

### 6.7

Data: 25/04/2023

- Atualizações de segurança / Facetec 9.6.25 / Melhorias de UX

### 6.6

Data: 04/04/2023

- Atualizações de segurança / Facetec 9.6.23

### 6.6

Data: 04/04/2023

- Correções de inicialização da Classe Liveness3DTextKey na Activity

### 6.5

- Correções de inicialização da Classe Liveness3DTextKey na Activity

### 6.4

- Melhorias de UX
- Correções de compatiblidade na importação da Classe Liveness3DTextKey

### 6.3

- Permitir customização das strings via objetos

### 6.2

Data: 13/03/2023

- Atualizações de segurança / Facetec 9.6.15

### 6.1

- Permitir customização da propriedade guidanceCustomizationReadyScreenHeaderFont

### 6.0

Data: 23/02/2023

##### Remoção das seguintes propriedades abaixo:

- guidanceCustomizationReadyScreenHeaderAttributedString
- guidanceCustomizationReadyScreenSubtextAttributedString
- guidanceCustomizationRetryScreenHeaderAttributedString
- guidanceCustomizationRetryScreenSubtextAttributedString

#### Novo formato para importar as dependências

- A partir da versão 6.0 somente é necessário declarar e importar o artefato do liveness 3D, não sendo mais necessário importar a lib da facetec paralelamente.

### 5.8.0

- Adicionado prevenção para clique duplo no botão de iniciar o liveness
- Permitir customização de botão habilitado/desabilitado
- Melhorias de UX

### 5.7.0

- Atualização da versão do Facetec SDK para 9.4.23
- Melhorias de UX
