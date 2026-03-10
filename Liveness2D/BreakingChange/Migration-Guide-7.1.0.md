# Guia de migração — DocumentsCopy SDK

## 7.0.0 → 7.1.0

Este guia descreve as mudanças necessárias para clientes que utilizam o fluxo **DocumentsCopy** ao atualizar do SDK **7.0.0** para **7.1.0**.

## Mudanças de comportamento (breaking changes)

### CNH Digital não vem mais habilitada por padrão

A partir da versão **7.1.0**, a opção **CNH Digital** deixou de aparecer automaticamente na tela de instruções.

Até a versão **7.0.0**, a CNH Digital vinha habilitada por padrão (comportamento equivalente a `true`).

Agora ela precisa ser habilitada explicitamente ao iniciar a `DocumentscopyActivity` via `Intent` extra (valor padrão `false`).

- Nova propriedade: `DocumentscopyActivity.PARAM_ENABLE_CNH_DIGITAL` (`"param_enable_cnh_digital"`)
- Valor padrão: `false`
- Se não enviar essa flag, a opção CNH Digital não é exibida
- Leitura no SDK (default `false`): DocumentscopyActivity.kt

**Como habilitar**

```kotlin
val intent = Intent(context, DocumentscopyActivity::class.java).apply {
    putExtra(DocumentscopyActivity.PARAM_ENVIRONMENT, Environment.HML)
    putExtra(DocumentscopyActivity.PARAM_APP_KEY, appKey)

    putExtra(DocumentscopyActivity.PARAM_ENABLE_CNH_DIGITAL, true)
}

startActivity(intent)
```

### Upload da CNH Digital agora aceita apenas PDF

O fluxo de CNH Digital agora aceita apenas arquivos PDF.

- Antes (7.0.0): `application/pdf`, `image/jpeg`, `image/png`
- Agora (7.1.0): `application/pdf`
- Implementação: DigitalCnhScreen.kt

## Novas funcionalidades

### Nova opção: Upload de documento via PDF (por arquivo)

Foi adicionada uma nova possibilidade de envio de documento via upload de arquivo PDF, exibida como uma terceira opção na tela de instruções (“Documento PDF”).

- Nova propriedade: `DocumentscopyActivity.PARAM_ENABLE_PDF_UPLOAD` (`"param_enable_pdf_upload"`)
- Valor padrão: `false`

**Como habilitar**

```kotlin
putExtra(DocumentscopyActivity.PARAM_ENABLE_PDF_UPLOAD, true)
```

**Propriedades de habilitação (Intent extras)**

- `DocumentscopyActivity.PARAM_ENABLE_CNH_DIGITAL` (`"param_enable_cnh_digital"`)
  - Até 7.0.0: comportamento padrão equivalente a `true`
  - 7.1.0: valor padrão `false`
- `DocumentscopyActivity.PARAM_ENABLE_PDF_UPLOAD` (`"param_enable_pdf_upload"`)
  - Nova propriedade na 7.1.0
  - Valor padrão `false`

Onde as opções são montadas: DocHomeFragment.kt

## Customização (tema)

### Nova tela de upload (PDF): DocumentFileScreenCustomBuilder

Foi introduzido um builder dedicado para customizar a tela de upload por arquivo:

- Classe: DocumentFileScreenCustomBuilder.kt
- Integração via `DocCopyTheme`: `setDocumentFileCustomsBuilder { ... }` (DocCopyTheme.kt)

**Exemplo**

```kotlin
val theme = DocCopyTheme.build {
    setDocumentFileCustomsBuilder {
        setUploadFileTitle("Envio de Arquivo")
        setUploadConfirmButtonText("Enviar")
    }
}
```

### Novas propriedades de customização (CNH Digital)

O builder `DigitalCnhScreenCustomBuilder` recebeu novas propriedades para personalizar a tela de upload:

- Área de seleção:
  - `setUploadSelectionAreaHintText(...)`
  - `setUploadAreaHeightDp(...)`
- Estado de sucesso após selecionar arquivo:
  - `setUploadSelectedFileSuccessText(...)`
  - `setUploadSelectedFileSuccessTextColor(...)`
  - `setUploadSelectedFileSuccessTextSizeSp(...)`
  - `setUploadSelectedFileSuccessIcon(...)`
  - `setUploadSelectedFileSuccessIconSizeDp(...)`

Referência: DigitalCnhScreenCustomBuilder.kt

### Instruções: customização da opção “Documento PDF”

O builder `DocCoreCustomInstructionsBuilder` ganhou propriedades para customizar a terceira opção quando `PARAM_ENABLE_PDF_UPLOAD=true`.

Referência: DocCoreCustomInstructionsBuilder.kt

## Fonts: chaves novas (DocCoreFontsKey)

O enum `DocCoreFontsKey` recebeu novas entradas para suportar a terceira opção (“Documento PDF”) e a tela de upload por arquivo:

- Tela de instruções (3ª opção):
  - `INSTRUCTIONS_DOCUMENT_THIRD_BUTTON_TITLE_FONT`
  - `INSTRUCTIONS_DOCUMENT_THIRD_BUTTON_CAPTION_FONT`
- CNH Digital:
  - `DIGITAL_CNH_SELECTED_FILE_CAPTION_FONT`
- Upload de documento (PDF):
  - `DOCUMENT_UPLOAD_TITLE_FONT`
  - `DOCUMENT_UPLOAD_CAPTION_FONT`
  - `DOCUMENT_UPLOAD_SELECT_FILE_FONT`
  - `DOCUMENT_UPLOAD_SELECTED_FILE_FONT`
  - `DOCUMENT_UPLOAD_SELECTED_FILE_CAPTION_FONT`
  - `DOCUMENT_UPLOAD_BUTTON_FONT`