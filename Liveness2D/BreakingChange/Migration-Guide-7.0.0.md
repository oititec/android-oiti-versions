# Migration Guide - 7.0.0

Este documento descreve, de forma objetiva, as mudanças com impacto de compatibilidade introduzidas na versão 7.0.0 do SDK e como adaptar projetos existentes.

## ⚠️ Resumo das Mudanças

**Impacto para integrações existentes**
- **Tela de Instruções (InstructionsScreen)**: API de customização alterada (novos builders). Chamadas antigas de customização dessa tela podem deixar de compilar.

**Funcionalidades novas (não quebram código atual)**
- **Fluxo de CNH Digital**: fluxo adicional de captura via documento digital (telas Permission, QR Code, Digital CNH, Processing e Result).

**Comportamento inalterado**
- **Fluxo de captura física**: após a seleção na tela de instruções, o fluxo de captura física continua utilizando os mesmos métodos do `DocCopyTheme.Builder`.

# Atualizações Importantes

## Requisito de Jetpack Compose

Na versão 7.0.0, o fluxo de CNH Digital (telas em Compose) foi implementado utilizando **Jetpack Compose**. Para que o SDK seja inicializado corretamente, o projeto que consome o SDK precisa ter Compose habilitado.

### Requisitos Mínimos

- **Kotlin**: Versão 2.1.21 ou superior
- **Plugin Compose**: `org.jetbrains.kotlin.plugin.compose` versão 2.1.21
- **Build Features**: `compose = true` no `build.gradle`

### Alterações Necessárias

Se seu projeto **não utiliza Compose**, você precisará adicionar a configuração mínima:

1. **Adicionar o plugin do Compose** no `build.gradle` do módulo principal:

```kotlin
plugins {
    id 'org.jetbrains.kotlin.plugin.compose' version '2.1.21'
}
```

2. **Habilitar Compose** nas `buildFeatures`:

```kotlin
android {
    buildFeatures {
        compose true
    }
}
```

3. **Adicionar o Compose BOM** (recomendado para garantir compatibilidade):

```kotlin
dependencies {
    implementation platform("androidx.compose:compose-bom:2025.01.01")
}
```

## Alterações no Sistema de Customização

Na versão 7.0.0, foi introduzido o **novo fluxo de CNH Digital** e a tela de instruções foi atualizada para permitir a escolha entre documento físico e digital. O fluxo de captura de documento físico (processamento/resultado) permanece utilizando os mesmos métodos do `DocCopyTheme.Builder` como antes.

### O que permanece igual

Os seguintes métodos do `DocCopyTheme.Builder` **continuam funcionando normalmente** para o fluxo de captura física:

- `setCaptureBackgroundColor()`
- `setCaptureInstructionGuideTextFront()`
- `setCaptureInstructionGuideTextBack()`
- `setTextConfirmation()`
- `setCaptureInstructionGuideReviewText()`
- `setCapturePreviewBorderColorForCapture()`
- `setBackgroundOkColor()`
- `setBackgroundDismissColor()`
- `setCaptureBottomSheetShapeColor()`
- `setCaptureBackButtonColorsIcon()`
- `setCaptureCloseButtonColorsIcon()`
- E outros métodos relacionados à captura física

**Exemplo de customização do fluxo físico (continua igual):**

```kotlin
// Este código continua funcionando exatamente como antes
val theme = DocCopyTheme.Builder()
    .setCaptureBackgroundColor("#333333")
    .setCaptureInstructionGuideTextFront("Posicione o documento")
    .setCaptureInstructionGuideTextBack("Vire o documento")
    .setTextConfirmation("Confirme a captura")
    .setCapturePreviewBorderColorForCapture("#FF0000")
    .setBackgroundOkColor("#4CAF50")
    .setBackgroundDismissColor("#F44336")
    .build()
```

### O que foi alterado

**Tela de Instruções (InstructionsScreen)** - Esta é a tela que afeta quem já utilizava o SDK:

A tela de instruções foi atualizada para permitir a escolha entre documento físico e digital. Os métodos antigos de customização desta tela foram removidos e substituídos pelo novo `DocCoreCustomInstructionsBuilder`.

### O que é novo

**Fluxo de CNH Digital** - Este é um fluxo completamente novo que não existia antes:

As seguintes telas são novas e fazem parte do fluxo de CNH Digital:
- **Permission** (permissão de câmera) - Nova
- **QR Code** (tela de QR Code) - Nova
- **Digital CNH** (upload de CNH digital) - Nova
- **Processing** (processamento do CNH Digital) - Nova
- **Result** (resultado do CNH Digital) - Nova

## Remoção de Métodos do `DocCopyTheme.Builder` - Tela de Instruções

Na versão 7.0.0, os métodos relacionados à customização da **tela de instruções** foram removidos e substituídos pelo novo `DocCoreCustomInstructionsBuilder`.

> **Importante**: Esta é a mudança que afeta quem já utilizava o SDK. A tela de instruções agora permite escolher entre documento físico e digital, e a forma de customização mudou.

### Métodos Removidos

- `setInstructionOptionDocumentText()`
- `setInstructionOptionDocumentTextColor()`
- `setInstructionOptionLightingText()`
- `setInstructionOptionLightingTextColor()`
- `setInstructionOptionDocumentIconColor()`
- `setInstructionOptionLightingIconColor()`
- `setInstructionContinueButtonBackgroundColor()`
- `setInstructionContinueButtonTextColor()`
- `setInstructionOptionDocumentBorderColor()`
- `setInstructionOptionDocumentBackgroundColor()`
- `setInstructionOptionDocumentTextFont()`
- `setInstructionOptionLightingBorderColor()`
- `setInstructionOptionLightingBackgroundColor()`
- `setInstructionContinueButtonTextFont()`
- `setInstructionOptionLightingTextFont()`

### Alterações Necessárias

Se sua aplicação utiliza esses métodos, atualize seu código para utilizar o novo `DocCoreCustomInstructionsBuilder` através do método `setInstructionsThemeBuilder()`.

**Código Antigo:**

```kotlin
private fun getNewTheme() = DocCopyTheme.Builder()
    .setInstructionOptionDocumentText("Documento Físico")
    .setInstructionOptionDocumentTextColor("#A5CD39")
    .setInstructionOptionLightingText("Iluminação")
    .setInstructionOptionLightingTextColor("#fc0000")
    .setInstructionOptionDocumentIconColor("#A5CD39")
    .setInstructionOptionLightingIconColor("#fc0000")
    .setInstructionOptionDocumentBorderColor("#fc0000")
    .setInstructionOptionDocumentBackgroundColor("#0E1979")
    .setInstructionOptionLightingBorderColor("#fc0000")
    .setInstructionOptionLightingBackgroundColor("#A5CD39")
    .setInstructionContinueButtonBackgroundColor("#FFFFFF")
    .setInstructionContinueButtonTextColor("#A5CD39")
    .build()
```

**Código Novo:**

```kotlin
private fun getNewTheme() = DocCopyTheme.Builder()
    .setInstructionsThemeBuilder {
        setInstructionPhysicalDocumentOptionTitle("Documento Físico")
        setInstructionPhysicalDocumentOptionTitleColor("#A5CD39")
        setInstructionPhysicalDocumentOptionDescription("Iluminação")
        setInstructionPhysicalDocumentOptionDescriptionColor("#fc0000")
        setInstructionPhysicalDocumentOptionIconColor("#A5CD39")
        setInstructionPhysicalDocumentOptionBorderColor("#fc0000")
        setInstructionPhysicalDocumentOptionBackgroundColor("#0E1979")
        setInstructionDigitalDocumentOptionTitle("Documento Digital")
        setInstructionDigitalDocumentOptionTitleColor("#fc0000")
        setInstructionDigitalDocumentOptionBackgroundColor("#A5CD39")
        setInstructionDigitalDocumentOptionBorderColor("#fc0000")
        setInstructionContinueButtonBackgroundColor("#FFFFFF")
        setInstructionContinueButtonTextColor("#A5CD39")
    }
    .build()
```

## Remoção de Propriedades do `DocCopyTheme` - Tela de Instruções

Na versão 7.0.0, as propriedades relacionadas à customização da **tela de instruções** foram removidas e substituídas pelo novo `DocCoreCustomInstructionsBuilder`.

> **Importante**: As propriedades e métodos relacionados à captura física de documento (após a seleção na tela de instruções) permanecem inalterados e continuam funcionando como antes.

### Propriedades Removidas

- `instructionBackButtonIcon`
- `instructionTitleText`
- `instructionTitleColor`
- `instructionCaptionText`
- `instructionCaptionColor`
- `instructionBackgroundColor`
- `instructionBottomSheetBackgroundColor`
- `instructionBottomSheetRadius`
- `rgButtonStoke`
- `rgButtonStokeColor`
- `rgCaptionText`
- `rgCaptionColor`
- `cnhButtonStoke`
- `cnhButtonStokeColor`
- `cnhCaptionText`
- `cnhCaptionColor`

### Alterações Necessárias

Se sua aplicação utiliza essas propriedades no construtor de `DocCopyTheme`, atualize seu código para utilizar os novos builders específicos.

**Código Antigo:**

```kotlin
val theme = DocCopyTheme(
    instructionTitleText = "Título",
    instructionTitleColor = Color.parseColor("#A5CD39"),
    instructionCaptionText = "Legenda",
    instructionCaptionColor = Color.parseColor("#A5CD39"),
    instructionBackgroundColor = Color.parseColor("#A5CD39"),
    instructionBottomSheetBackgroundColor = Color.parseColor("#333333"),
    instructionBottomSheetRadius = 20,
    rgButtonStoke = Color.parseColor("#000000"),
    rgCaptionText = "Texto RG"
)
```

**Código Novo:**

```kotlin
val theme = DocCopyTheme.Builder()
    .setInstructionsThemeBuilder {
        setInstructionTitle("Título")
        setInstructionTitleColor("#A5CD39")
        setInstructionCaption("Legenda")
        setInstructionCaptionColor("#A5CD39")
        setInstructionBackgroundColor("#A5CD39")
        setInstructionBottomSheetColor("#333333")
        setInstructionBottomSheetCornerRadius(20f)
    }
    .build()
```

## Nova Forma de Customização com Builders Específicos

### Tela de Instruções (Alterada)

A tela de instruções agora utiliza o `DocCoreCustomInstructionsBuilder` para customização. Esta é a mudança que afeta quem já utilizava o SDK.

### Fluxo de CNH Digital (Novo)

Introduzimos builders dedicados para cada tela do **novo fluxo de CNH Digital**. Para setar a customização, criamos um builder e passamos no parâmetro `PARAM_THEME`.

> **Importante**: 
> - A **tela de instruções** foi alterada e agora utiliza `DocCoreCustomInstructionsBuilder`
> - O **fluxo de CNH Digital** é novo e utiliza os novos builders específicos
> - O **fluxo de captura física** (após a seleção) continua utilizando os métodos tradicionais do `DocCopyTheme.Builder`

```kotlin
putExtra(DocumentscopyActivity.PARAM_THEME, getNewTheme())
```

### Builders Disponíveis

- `DocCoreCustomInstructionsBuilder` - Tela de seleção (físico/digital)
- `PermissionCustomsBuilder` - Tela de permissão de câmera
- `DigitalCnhScreenCustomBuilder` - Tela de upload de CNH digital
- `QrScreenCustomBuilder` - Tela de QR Code
- `ProcessingCustomsBuilder` - Tela de processamento
- `ResultCustomsBuilder` - Tela de resultado

### Exemplo de Customização Completa

```kotlin
private fun getNewTheme() = DocCopyTheme.Builder()
    // Configurações do fluxo de captura física (permanecem iguais)
    .setCaptureBackgroundColor("#333333")
    .setCaptureInstructionGuideTextFront("ARO GuideText")
    .setCaptureInstructionGuideTextBack("ARO GuideText Back")
    .setTextConfirmation("ARO123222")
    .setCapturePreviewBorderColorForCapture("#FF0000")
    .setBackgroundOkColor("#000000")
    .setBackgroundDismissColor("#333333")
    .setCaptureBottomSheetShapeColor("#A5CD39")
    .setCaptureBackButtonColorsIcon("#A5CD39")
    .setCaptureCloseButtonColorsIcon("#A5CD39")
    
    // Tela de Instruções (ALTERADA - agora permite escolher físico/digital)
    .setInstructionsThemeBuilder {
        setInstructionBackgroundColor("#FF0000")
        setInstructionBottomSheetColor("#FF00FF")
        setInstructionBottomSheetCornerRadius(20f)
        setInstructionTitle("Título Exemplo")
        setInstructionTitleColor("#FF5733")
        setInstructionCaption("Legenda Exemplo")
        setInstructionCaptionColor("#33FF57")
        setInstructionPhysicalDocumentOptionTitle("Documento Físico")
        setInstructionPhysicalDocumentOptionTitleColor("#5733FF")
        setInstructionDigitalDocumentOptionTitle("Documento Digital")
        setInstructionDigitalDocumentOptionTitleColor("#0000FF")
    }
    
    // Tela de Permissão (NOVA - parte do fluxo CNH Digital)
    .setPermissionCustomsBuilder {
        setBackgroundColor("#1A1A1A")
        setTitle("Permissão de Câmera")
        setTitleColor("#FFFFFF")
        setSubTitle("Precisamos acessar sua câmera para capturar o documento")
        setSubTitleColor("#CCCCCC")
        setPermissionButtonText("Permitir Acesso")
        setPermissionButtonColor("#4CAF50")
        setPermissionButtonTextColor("#FFFFFF")
    }
    
    // Tela de CNH Digital (NOVA - upload de arquivo)
    .setDigitalCnhCustomsBuilder {
        setUploadBackgroundColor("#1A1A1A")
        setUploadFileTitle("Envio de Documento")
        setUploadFileTitleColor("#FFFFFF")
        setUploadFileDescription("Selecione o arquivo da CNH digital em PDF, JPEG ou PNG")
        setUploadFileDescriptionColor("#CCCCCC")
        setUploadConfirmButtonText("Enviar Documento")
        setUploadConfirmButtonTextColor("#FFFFFF")
        setUploadConfirmButtonBackgroundColor("#1B1BD1")
    }
    
    // Tela de QR Code (NOVA - parte do fluxo CNH Digital)
    .setQrCodeCustomsBuilder {
        setQrCodeBottomSheetColor("#F5F5F5")
        setQrCodeBottomSheetCornerRadius(30f)
        setQrCodeTitle("Não conseguiu escanear?")
        setQrCodeTitleColor("#1A1A1A")
        setQrCodeCaption("Envie o documento de outra forma")
        setQrCodeCaptionColor("#666666")
        setQrCodeFileButtonText("Fazer upload do arquivo")
        setQrCodeFileButtonTextColor("#FFFFFF")
        setQrCodeFileButtonBackgroundColor("#FF5722")
    }
    
    // Tela de Processamento (NOVA - parte do fluxo CNH Digital)
    .setProcessingCustomsBuilder {
        setBackgroundColor("#1A1A1A")
        setLoadingDialogColor("#4CAF50")
        setLoadingIndicatorSize(80)
        setStatusBarColor("#000000")
        setStatusBarIsDarkIcons(false)
    }
    
    // Tela de Resultado (NOVA - parte do fluxo CNH Digital)
    .setResultCustomsBuilder {
        setSuccessBackgroundColor("#4CAF50")
        setSuccessText("Documento enviado com sucesso!")
        setSuccessTextColor("#FFFFFF")
        setErrorBackgroundColor("#F44336")
        setErrorText("Erro ao enviar documento")
        setErrorTextColor("#FFFFFF")
        setRetryButtonText("Tentar Novamente")
        setRetryButtonTextColor("#FFFFFF")
    }
    .build()
```

## Nova Forma de Customização de Fontes

Introduzimos uma nova forma de customizar fontes de todas as telas através de um `HashMap<DocCoreFontsKey, String>`.

```kotlin
val docCoreFontsKey = hashMapOf(
    DocCoreFontsKey.INSTRUCTIONS_TITLE_FONT to "fonts/sixty.ttf",
    DocCoreFontsKey.INSTRUCTIONS_CAPTION_FONT to "fonts/sixty.ttf",
    DocCoreFontsKey.INSTRUCTIONS_DOCUMENT_FIRST_BUTTON_TITLE_FONT to "fonts/sixty.ttf",
    DocCoreFontsKey.INSTRUCTIONS_DOCUMENT_FIRST_BUTTON_CAPTION_FONT to "fonts/sixty.ttf",
    DocCoreFontsKey.INSTRUCTIONS_DOCUMENT_SECOND_BUTTON_TITLE_FONT to "fonts/sixty.ttf",
    DocCoreFontsKey.INSTRUCTIONS_DOCUMENT_SECOND_BUTTON_CAPTION_FONT to "fonts/sixty.ttf",
    
    DocCoreFontsKey.PERMISSION_TITLE_FONT to "fonts/sixty.ttf",
    DocCoreFontsKey.PERMISSION_CAPTION_FONT to "fonts/sixty.ttf",
    DocCoreFontsKey.PERMISSION_BUTTON_FONT to "fonts/sixty.ttf",
    
    DocCoreFontsKey.QR_BOTTOM_SHEET_TITLE_FONT to "fonts/sixty.ttf",
    DocCoreFontsKey.QR_BOTTOM_SHEET_CAPTION_FONT to "fonts/sixty.ttf",
    DocCoreFontsKey.QR_BOTTOM_SHEET_BUTTON_FONT to "fonts/sixty.ttf",
    
    DocCoreFontsKey.DIGITAL_CNH_TITLE_FONT to "fonts/sixty.ttf",
    DocCoreFontsKey.DIGITAL_CNH_CAPTION_FONT to "fonts/sixty.ttf",
    DocCoreFontsKey.DIGITAL_CNH_SELECT_FILE_FONT to "fonts/sixty.ttf",
    DocCoreFontsKey.DIGITAL_CNH_SELECTED_FILE_FONT to "fonts/sixty.ttf",
    DocCoreFontsKey.DIGITAL_CNH_BUTTON_FONT to "fonts/sixty.ttf",
    
    DocCoreFontsKey.RESULT_MESSAGE_FONT to "fonts/sixty.ttf",
    DocCoreFontsKey.RESULT_RETRY_BUTTON_FONT to "fonts/sixty.ttf"
)

intent.putExtra(DocumentscopyActivity.PARAM_FONTS, docCoreFontsKey)
```

### Alterações Necessárias

Se sua aplicação customiza fontes, atualize seu código para utilizar o novo sistema de `DocCoreFontsKey`.
